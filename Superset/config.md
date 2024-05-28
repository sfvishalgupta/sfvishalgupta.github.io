#### [Back](./README.md)

# Apache Superset Config

### Setup App Name
```python
APP_NAME = "Sourcefuse"
```

### Setup Logo Tooltip
```python
LOGO_TOOLTIP = "Sourcefuse"
```

### Setup Theme
```python
THEME_OVERRIDES = {
    "colors": {
        "text": {
            "label": '#879399',
            "help": '#737373'
        },
        "primary": {
            "base": 'red',
        },
        "secondary": {
            "base": 'green',
        },
        "grayscale": {
            "base": 'orange',
        },
        "error":{
            "base": 'Pink'
        }
    },
    "typography": {
        "families": {
        "sansSerif": 'Inter',
        "serif": 'Georgia',
        "monospace": 'Fira Code',
        },
        "weights": {
            "light": 200,
            "normal": 400,
            "medium": 500,
            "bold": 600
        }
	}
}
```

### Setup Preferred Databases
```python
PREFERRED_DATABASES: list[str] = [
    "PostgreSQL",
    "Presto",
    "MySQL",
    "SQLite",
]
```

### Setup Databases Images
```python
DB_IMAGES:
  postgresql: "path/to/image/postgres.jpg"
  bigquery: "path/to/s3bucket/bigquery.jpg"
  snowflake: "path/to/image/snowflake.jpg"
```


### Enable Debugging
```
FLASK_DEBUG=True
```

### Enable/Disable CSRF protection (superset/config.py)
```python
WTF_CSRF_ENABLED = True
```

### Disable Example DB
```bash
SUPERSET_LOAD_EXAMPLES=yes
```

### Authentication Config (AUTH_TYPE)
Below are the Authentication Type
1. AUTH_OID : Is for OpenID
2. AUTH_DB : Is for database (username/password)
3. AUTH_LDAP : Is for LDAP
4. AUTH_REMOTE_USER : Is for using REMOTE_USER from web server
5. AUTH_OAUTH : For OAuth

### Enable OAuth
```bash
AUTH_TYPE=AUTH_OAUTH
```

### Registration Config (Allow Self Registration)
```bash
AUTH_USER_REGISTRATION = True
```

### List of OAuth Providers
```python
OAUTH_PROVIDERS = [
    {
        "name": "twitter",
        "icon": "fa-twitter",
        "token_key": "oauth_token",
        "remote_app": {
            "client_id": "TWITTER_KEY",
            "client_secret": "TWITTER_SECRET",
            "api_base_url": "https://api.twitter.com/1.1/",
            "request_token_url": "https://api.twitter.com/oauth/request_token",
            "access_token_url": "https://api.twitter.com/oauth/access_token",
            "authorize_url": "https://api.twitter.com/oauth/authenticate",
        },
    },
    {
        "name": "google",
        "icon": "fa-google",
        "token_key": "access_token",
        "remote_app": {
            "client_id": "GOOGLE_KEY",
            "client_secret": "GOOGLE_SECRET",
            "api_base_url": "https://www.googleapis.com/oauth2/v2/",
            "client_kwargs": {"scope": "email profile"},
            "request_token_url": None,
            "access_token_url": "https://accounts.google.com/o/oauth2/token",
            "authorize_url": "https://accounts.google.com/o/oauth2/auth",
            "jwks_uri": "https://www.googleapis.com/oauth2/v3/certs",
        },
    },
    {
        "name": "openshift",
        "icon": "fa-circle-o",
        "token_key": "access_token",
        "remote_app": {
            "client_id": "system:serviceaccount:mynamespace:mysa",
            "client_secret": "<mysa serviceaccount token here>",
            "api_base_url": "https://openshift.default.svc.cluster.local:443",
            "client_kwargs": {"scope": "user:info"},
            "redirect_uri": "https://myapp-mynamespace.apps.<cluster_domain>",
            "access_token_url": "https://oauth-openshift.apps.<cluster_domain>/oauth/token",
            "authorize_url": "https://oauth-openshift.apps.<cluster_domain>/oauth/authorize",
            "token_endpoint_auth_method": "client_secret_post",
        },
    },
    {
        "name": "okta",
        "icon": "fa-circle-o",
        "token_key": "access_token",
        "remote_app": {
            "client_id": "OKTA_KEY",
            "client_secret": "OKTA_SECRET",
            "api_base_url": "https://OKTA_DOMAIN.okta.com/oauth2/v1/",
            "client_kwargs": {"scope": "openid profile email groups"},
            "access_token_url": "https://OKTA_DOMAIN.okta.com/oauth2/v1/token",
            "authorize_url": "https://OKTA_DOMAIN.okta.com/oauth2/v1/authorize",
            "server_metadata_url": f"https://OKTA_DOMAIN.okta.com/.well-known/openid-configuration",
        },
    },
    {
        "name": "aws_cognito",
        "icon": "fa-amazon",
        "token_key": "access_token",
        "remote_app": {
            "client_id": "COGNITO_CLIENT_ID",
            "client_secret": "COGNITO_CLIENT_SECRET",
            "api_base_url": "https://COGNITO_APP.auth.REGION.amazoncognito.com/",
            "client_kwargs": {"scope": "openid email aws.cognito.signin.user.admin"},
            "access_token_url": "https://COGNITO_APP.auth.REGION.amazoncognito.com/token",
            "authorize_url": "https://COGNITO_APP.auth.REGION.amazoncognito.com/authorize",
        },
    },
    {
        "name": "keycloak",
        "icon": "fa-key",
        "token_key": "access_token",
        "remote_app": {
            "client_id": "KEYCLOAK_CLIENT_ID",
            "client_secret": "KEYCLOAK_CLIENT_SECRET",
            "api_base_url": "https://KEYCLOAK_DOMAIN/realms/master/protocol/openid-connect",
            "client_kwargs": {
                "scope": "email profile"
            },
            "access_token_url": "KEYCLOAK_DOMAIN/realms/master/protocol/openid-connect/token",
            "authorize_url": "KEYCLOAK_DOMAIN/realms/master/protocol/openid-connect/auth",
            "request_token_url": None,
        },
    },
    {
        "name": "keycloak_before_17",
        "icon": "fa-key",
        "token_key": "access_token",
        "remote_app": {
            "client_id": "KEYCLOAK_CLIENT_ID",
            "client_secret": "KEYCLOAK_CLIENT_SECRET",
            "api_base_url": "https://KEYCLOAK_DOMAIN/auth/realms/master/protocol/openid-connect",
            "client_kwargs": {
                "scope": "email profile"
            },
            "access_token_url": "KEYCLOAK_DOMAIN/auth/realms/master/protocol/openid-connect/token",
            "authorize_url": "KEYCLOAK_DOMAIN/auth/realms/master/protocol/openid-connect/auth",
            "request_token_url": None,
        },
    },
    {
        "name": "azure",
        "icon": "fa-windows",
        "token_key": "access_token",
        "remote_app": {
            "client_id": "AZURE_APPLICATION_ID",
            "client_secret": "AZURE_SECRET",
            "api_base_url": "https://login.microsoftonline.com/AZURE_TENANT_ID/oauth2",
            "client_kwargs": {
                "scope": "User.read name preferred_username email profile upn",
                "resource": "AZURE_APPLICATION_ID",
                # Optionally enforce signature JWT verification
                "verify_signature": False
            },
            "request_token_url": None,
            "access_token_url": "https://login.microsoftonline.com/AZURE_TENANT_ID/oauth2/token",
            "authorize_url": "https://login.microsoftonline.com/AZURE_TENANT_ID/oauth2/authorize",
        },
    },
]
```

