#### [Back](./README.md)

# Setup OAuth Apache Superset

### Packages Needs to install
1. flask-appbuilder
1. Authlib

### Add below config in superset_config.py
```python
from custom_sso_security_manager import CustomSsoSecurityManager
from flask_appbuilder.security.manager import AUTH_OAUTH

AUTH_TYPE = AUTH_OAUTH
AUTH_USER_REGISTRATION = True
AUTH_USER_REGISTRATION_ROLE = "Public"

OKTA_BASE_URL = "https://dev-82570728.okta.com"
OAUTH_PROVIDERS = [
    {
        "name": "okta",
        "token_key": "access_token",
        "icon": "fa-circle-o",
        "remote_app": {
            "client_id": "0oagx182a4d0NvwF15d7",
            "client_secret": "7MVtdGmr2zNNAprS8TVqqcmSafKQj3adTSWNSdTKTDAxT9mUwwg0JHjK-wnw1fUB",
            "client_kwargs": {"scope": "openid profile email"},
            "access_token_method": "POST",
            "api_base_url": f"{OKTA_BASE_URL}/oauth2/v1/",
            "access_token_url": f"{OKTA_BASE_URL}/oauth2/v1/token",
            "authorize_url": f"{OKTA_BASE_URL}/oauth2/v1/authorize",
            "server_metadata_url": f"{OKTA_BASE_URL}/.well-known/openid-configuration",
        },
    },
]
CUSTOM_SECURITY_MANAGER = CustomSsoSecurityManager
```

### To customize the userinfo retrieval, you can create your own method like this:
```python
@appbuilder.sm.oauth_user_info_getter
def my_user_info_getter(
    sm: SecurityManager,
    provider: str,
    response: Dict[str, Any]
) -> Dict[str, Any]:
    if provider == "okta":
        me = sm.oauth_remotes[provider].get("userinfo")
        return {
            "username": "okta_" + me.data.get("sub", ""),
            "first_name": me.data.get("given_name", ""),
            "last_name": me.data.get("family_name", ""),
            "email": me.data.get("email", ""),
            "role_keys": me.data.get("groups", []),
        }
    return {}
```