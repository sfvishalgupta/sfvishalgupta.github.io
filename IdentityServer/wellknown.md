#### [Back](./README.md)

# Server Discovery Endpoints(Well Knowns)

OpenID providers publish their metadata at a well-known URL. 

## Metadata Values

* **issuer** 
The Issuer Identifier of the OpenID Connect Provider. This value is the same as the iss claim value in the ID tokens issued by this provider.

* **authorization_endpoint** 
The URL of the OpenID Connect Provider's OAuth 2.0 Authorization Endpoint.

* **token_endpoint** 
The URL of the OpenID Connect Provider's OAuth 2.0 Token Endpoint.

* **userinfo_endpoint** 
The URL of the OpenID Connect Provider's UserInfo Endpoint.

* **jwks_uri** 
The URL of the OpenID Connect Provider's JSON Web Key Set document. This document contains signing keys that clients use to validate the signatures from the provider.

* **scopes_supported** 
A JSON array containing a list of OAuth 2.0 scope values configured in this provider.

* **response_types_supported** 
A JSON array containing a list of OAuth 2.0 response types supported by this provider.

* **response_modes_supported** 
A JSON array containing a list of OAuth 2.0 response modes supported by this provider.

* **grant_types_supported** 
A JSON array containing a list of OAuth 2.0 grant types supported by this provider.

* **subject_types_supported** 
A JSON array containing a list of Subject Identifier types supported by this provider.

* **id_token_signing_alg_values_supported** 
A JSON array containing a list of the JWS signing algorithms (alg values) supported by this provider for the ID Token to encode the Claims in a JWT.

* **id_token_encryption_alg_values_supported** 
A JSON array containing a list of the JWE encryption algorithms (alg values) supported by this provider for the ID Token to encode the Claims in a JWT.

* **id_token_encryption_enc_values_supported** 
A JSON array containing a list of the JWE encryption algorithms (enc values) supported by this provider for the ID Token to encode the Claims in a JWT.

* **token_endpoint_auth_methods_supported** 
A JSON array containing a list of Client Authentication methods supported by this Token Endpoint.

* **token_endpoint_auth_signing_alg_values_supported** 
A JSON array containing a list of the JWS signing algorithms (alg values) supported by this Token Endpoint for the signature on the JWT used to authenticate the Client at the Token Endpoint for the private_key_jwt and client_secret_jwt authentication methods.

* **claims_parameter_supported** 
Boolean value specifying whether this provider supports use of the claims parameter. A value of true indicates support. If omitted, the default value is false.

* **request_parameter_supported** 
Boolean value specifying whether this provider supports use of the request parameter. A value of true indicates support. If omitted, the default value is false.

* **request_uri_parameter_supported** 
Boolean value specifying whether this provider supports use of the request_uri parameter. A value of true indicates support. If omitted, the default value is true.


## Example of Well Knowns

1. <a href="https://dev-599740.okta.com/oauth2/default/.well-known/oauth-authorization-server" target="_blank">OKTA</a>

```json
{
  "issuer": "https://dev-599740.okta.com/oauth2/default",
  "authorization_endpoint": "https://dev-599740.okta.com/oauth2/default/v1/authorize",
  "token_endpoint": "https://dev-599740.okta.com/oauth2/default/v1/token",
  "registration_endpoint": "https://dev-599740.okta.com/oauth2/v1/clients",
  "jwks_uri": "https://dev-599740.okta.com/oauth2/default/v1/keys",
  "response_types_supported": [
    "code",
    "token",
    "id_token",
    "code id_token",
    "code token",
    "id_token token",
    "code id_token token"
  ],
  "response_modes_supported": [
    "query",
    "fragment",
    "form_post",
    "okta_post_message"
  ],
  "grant_types_supported": [
    "authorization_code",
    "implicit",
    "refresh_token",
    "password",
    "client_credentials",
    "urn:ietf:params:oauth:grant-type:device_code"
  ],
  "subject_types_supported": [
    "public"
  ],
  "scopes_supported": [
    "openid",
    "profile",
    "email",
    "address",
    "phone",
    "offline_access",
    "device_sso"
  ],
  "token_endpoint_auth_methods_supported": [
    "client_secret_basic",
    "client_secret_post",
    "client_secret_jwt",
    "private_key_jwt",
    "none"
  ],
  "claims_supported": [
    "ver",
    "jti",
    "iss",
    "aud",
    "iat",
    "exp",
    "cid",
    "uid",
    "scp",
    "sub"
  ],
  "code_challenge_methods_supported": [
    "S256"
  ],
  "introspection_endpoint": "https://dev-599740.okta.com/oauth2/default/v1/introspect",
  "introspection_endpoint_auth_methods_supported": [
    "client_secret_basic",
    "client_secret_post",
    "client_secret_jwt",
    "private_key_jwt",
    "none"
  ],
  "revocation_endpoint": "https://dev-599740.okta.com/oauth2/default/v1/revoke",
  "revocation_endpoint_auth_methods_supported": [
    "client_secret_basic",
    "client_secret_post",
    "client_secret_jwt",
    "private_key_jwt",
    "none"
  ],
  "end_session_endpoint": "https://dev-599740.okta.com/oauth2/default/v1/logout",
  "request_parameter_supported": true,
  "request_object_signing_alg_values_supported": [
    "HS256",
    "HS384",
    "HS512",
    "RS256",
    "RS384",
    "RS512",
    "ES256",
    "ES384",
    "ES512"
  ],
  "device_authorization_endpoint": "https://dev-599740.okta.com/oauth2/default/v1/device/authorize",
  "dpop_signing_alg_values_supported": [
    "RS256",
    "RS384",
    "RS512",
    "ES256",
    "ES384",
    "ES512"
  ]
}
```

2. <a href="https://cognito-idp.eu-west-1.amazonaws.com/eu-west-1_CUdISnM7M/.well-known/openid-configuration" target="_blank">AWS</a>
```json
{
  "authorization_endpoint": "https://pentairdealerqa.auth.eu-west-1.amazoncognito.com/oauth2/authorize",
  "end_session_endpoint": "https://pentairdealerqa.auth.eu-west-1.amazoncognito.com/logout",
  "id_token_signing_alg_values_supported": [
    "RS256"
  ],
  "issuer": "https://cognito-idp.eu-west-1.amazonaws.com/eu-west-1_CUdISnM7M",
  "jwks_uri": "https://cognito-idp.eu-west-1.amazonaws.com/eu-west-1_CUdISnM7M/.well-known/jwks.json",
  "response_types_supported": [
    "code",
    "token"
  ],
  "revocation_endpoint": "https://pentairdealerqa.auth.eu-west-1.amazoncognito.com/oauth2/revoke",
  "scopes_supported": [
    "openid",
    "email",
    "phone",
    "profile"
  ],
  "subject_types_supported": [
    "public"
  ],
  "token_endpoint": "https://pentairdealerqa.auth.eu-west-1.amazoncognito.com/oauth2/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_basic",
    "client_secret_post"
  ],
  "userinfo_endpoint": "https://pentairdealerqa.auth.eu-west-1.amazoncognito.com/oauth2/userInfo"
}
```