#### [Back](./README.md)

# AWS Cognito

Amazon Cognito provides authentication, authorization, and user management for your web and mobile apps. Your users can sign in directly with a user name and password, or through a third party such as Facebook, Amazon, Google or Apple.
The two main components of Amazon Cognito are user pools and identity pools. User pools are user directories that provide sign-up and sign-in options for your app users. Identity pools enable you to grant your users access to other AWS services. You can use identity pools and user pools separately or together.

**An Amazon Cognito user pool and identity pool used together**

See the diagram for a common Amazon Cognito scenario. Here the goal is to authenticate your user, and then grant your user access to another AWS service.
In the first step your app user signs in through a user pool and receives user pool tokens after a successful authentication.
Next, your app exchanges the user pool tokens for AWS credentials through an identity pool.
Finally, your app user can then use those AWS credentials to access other AWS services such as Amazon S3 or DynamoDB.

**Features of Amazon Cognito**

**User pools**

A user pool is a user directory in Amazon Cognito. With a user pool, your users can sign in to your web or mobile app through Amazon Cognito, or federate through a third-party identity provider (IdP). Whether your users sign in directly or through a third party, all members of the user pool have a directory profile that you can access through an SDK.

User pools provide:

* Sign-up and sign-in services.
* A built-in, customizable web UI to sign in users.
* Social sign-in with Facebook, Google, Login with Amazon, and Sign in with Apple, and through SAML and OIDC identity providers from your user pool.
* User directory management and user profiles.
* Security features such as multi-factor authentication (MFA), checks for compromised credentials, account takeover protection, and phone and email verification.
* Customized workflows and user migration through AWS Lambda triggers.

**Identity pools**

With an identity pool, your users can obtain temporary AWS credentials to access AWS services, such as Amazon S3 and DynamoDB. Identity pools support anonymous guest users, as well as the following identity providers that you can use to authenticate users for identity pools:

* Amazon Cognito user pools
* Social sign-in with Facebook, Google, Login with Amazon, and Sign in with Apple
* OpenID Connect (OIDC) providers
* SAML identity providers
* Developer authenticated identities

To save user profile information, your identity pool needs to be integrated with a user pool.