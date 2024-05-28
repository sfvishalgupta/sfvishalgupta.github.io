#### [Back](./README.md)

# Setup Apache Superset

### Clone Superset
```bash
git clone https://github.com/apache/superset.git
```

### Connect to Host Machine Postgres
update in docker/.env-non-dev file
```python
DATABASE_DB=superset_sourcefuse
DATABASE_HOST=host.docker.internal
DATABASE_PASSWORD=admin
DATABASE_USER=postgres
```

### Add Superset backend Folder as Volume
```yml
x-superset-volumes:
  &superset-volumes # /app/pythonpath_docker will be appended to the PYTHONPATH in the final container
  - ./docker:/app/docker
  - ./superset:/app/superset
  - superset_home:/app/superset_home
```

### Port Mapping
file **docker-compose-non-dev.yml**
```yml
superset:
    env_file: docker/.env-non-dev
    image: *superset-image
    container_name: sf_superset_app
    command: ["/app/docker/docker-bootstrap.sh", "app"]
    user: "root"
    restart: unless-stopped
    ports:
      - 80:8088
    depends_on: *superset-depends-on
    volumes: *superset-volumes
```

### Adding New Package
file **docker/requirement-local.txt**
```txt
boto3       ## for AWS
prophet     ## for Predictions
```


### Add endpoint to CSRF Exemption List (superset/config.py)
```python
WTF_CSRF_EXEMPT_LIST = [
    "superset.views.core.log",
    "superset.views.core.explore_json",
    "superset.charts.data.api.data",
    "superset.sfrestapi.api.test_post",
]
```

### Start Superset
```bash
docker compose -f docker-compose-non-dev.yml up
```

### Go into Docker
```bash
docker exec -it <container_name> bash
```

### List Installed Packages
```bash
pip freeze
```

### Superset URL
[localhost](http://localhost)

### Superset Swagger URL
[Swagger](http://localhost/swagger/v1)


Apply changes to the configuration file **docker/pythonpath_dev/superset_config.py**


### Adding new API to Superset Backend.
* Creating SFRestAPI Example
* Create new folder in **superset/sfRestAPI**
* Create new file **api.py** inside the folder with class name **SFRestAPI**.
```python
class SFRestAPI(BaseSupersetApi):
    class_permission_name = "AdvancedDataType"
    method_permission_name = MODEL_API_RW_METHOD_PERMISSION_MAP
    resource_name = "sfrestapi"
    allow_browser_login = True
    openapi_spec_tag = "SF Rest API"

    @expose("/test", methods=("GET",))
    @protect()
    @safe
    @statsd_metrics
    @event_logger.log_this
    def get(self) -> Response:
        return json_success(
            json.dumps(
                {"result": {"message": "hi"}},
                default=utils.json_iso_dttm_ser,
                ignore_nan=True,
            ),
            200,
        )
```

* Add entry of **SFRestAPI** in **superset/initialization/__init__.py** 
```python
appbuilder.add_api(SFRestAPI)
```

* Path for above api will be **/api/v1/sfrestapi/test**


### Updating Frontend Folder
* Mounting frontend folder and remove from depends
* Run below command after change frontend fils
```bash
npm run build
```
* OR build with watch
```bash
npm run dev
```

## Enable Public Rest API Reading
We can enable creating chart from Rest API by below configuration.

Add below packages in file *docker/requirement-local.txt*
```bash
shillelagh
shillelagh[all]
```

Add new Database Connection with below SQLALCHEMY URL
```bash
shillelagh+safe://
```

We also need to below JSON in *Engine Parameters* in *Advance Other* 
```json
{
    "connect_args":{
        "adapters":[
            "genericjsonapi"
            ]
        },
        "adapter_kwargs": {
            "genericjsonapi": {
                "request_headers": {
                    "X-Auth-Token": "SECRET",
                },
            },
        }
    }
```

OR we can pass in the url as below
```bash
https://api.example.com/?_s_headers=(X-Auth-Token:SECRET)s
```

Other list of Available Adapters are 
```bash
datasetteapi,
genericjsonapi,
githubapi,
htmltableapi,
s3selectapi,
socrataapi,
weatherapi
```

### Extra Adapter arguments
* **Reading files from S3**
```json
{
  "connect_args": {
    "adapters": [
      "s3selectapi"
    ],
    "adapter_kwargs": {
      "s3selectapi": {
        "aws_access_key_id": "XXX",
        "aws_secret_access_key": "YYY"
      }
    }
  }
}
```

* <b>Github</b>
```json
{
  "connect_args": {
    "adapters": [
      "githubapi"
    ],
    "adapter_kwargs": {
      "githubapi": {
        "access_token": "XXX"
      }
    }
  }
}
```

* <b>Weather Data</b>
```json
{
  "connect_args": {
    "adapters": [
      "weatherapi"
    ],
    "adapter_kwargs": {
      "weatherapi": {
        "api_key": "XXX"
      }
    }
  }
}
```


## Enable Dashboard Role
if you enable *DASHBOARD_RBAC* feature flag then you be able to manage which roles can access the dashboard.
- Granting a role access to a dashboard will bypass dataset level checks. Having dashboard access implicitly grants read access to all the featured charts in the dashboard, and thereby also all the associated datasets.
- If no roles are specified for a dashboard, regular Dataset permissions will apply.

## Customizing Dashboard
The following URL parameters can be used to modify how the dashboard is rendered:

- **standalone:**

    0 (default): dashboard is displayed normally

    1: Top Navigation is hidden

    2: Top Navigation + title is hidden

    3: Top Navigation + title + top level tabs are hidden
- **show_filters:**

    0: render dashboard without Filter Bar

    1 (default): render dashboard with Filter Bar if native filters are enabled
- **expand_filters:**
    (default): render dashboard with Filter Bar expanded if there are native filters

    0: render dashboard with Filter Bar collapsed

    1: render dashboard with Filter Bar expanded

## Setup Email Reporting

### Enable Email Reporting
Turn **ALERT_REPORTS** feature flag to True in **superset_config.py** or **superset_config_docker.py**.

### Disable Dry-Run Mode
Turn **ALERT_REPORTS_NOTIFICATION_DRY_RUN** feature flag to **False**.

### Email Configuration
- Below is the SMTP configuration in **superset_config.py**
```python
EMAIL_NOTIFICATIONS = True
SMTP_HOST = 'smtp.yourdomain.com'
SMTP_STARTTLS = True
SMTP_SSL = False
SMTP_USER = 'your_email@yourdomain.com'
SMTP_PORT = 587
SMTP_PASSWORD = 'your_password'
SMTP_MAIL_FROM = 'superset@yourdomain.com'
```
- **Celery Configuration:** Ensure that Celery is configured to send emails.
```python
CELERY_CONFIG = {
  'broker_url': 'redis://redis:6379/0',
  'result_backend': 'redis://redis:6379/0',
  'beat_schedule': {
    'email_reports': {
      'task': 'email_reports.send',
      'schedule': crontab(minute='*', hour='*')
    }
  }
}
```


* Adding Pretext with column 
```bash
("pretext" || column)
```