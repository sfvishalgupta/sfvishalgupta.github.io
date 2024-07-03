#### [Back](./README.md)

### REST API for user & role management
Flask-AppBuilder supports a REST API for user CRUD,
but this feature is in beta and is not enabled by default in Superset.
To enable this feature, set the following in your Superset configuration:

```python
FAB_ADD_SECURITY_API = True
```

Once configured, the documentation for additional "Security" endpoints will be visible in Swagger for you to explore.