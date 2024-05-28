#### [Back](./README.md)

# Tokens

## ID Tokens
ID Token is proof of user's authentication which is passed to application as proof that user is authenticated.

## Access Tokens
Access Token is the artifact that allows the client application to access the specific resource to perform specific actions on behalf of user.

That is what is known as **delegated authorization scenario**. the user delegates a client application to access the resource on their behalf.

**Example**
that you can authorize your LinkedIn app to access Twitter’s API on your behalf to cross-post on both social platforms. Keep in mind that you only authorize LinkedIn to publish your posts on Twitter. You don't authorize it to delete them or change your profile’s data or do other things, too. This limitation is very important in a delegated authorization scenario and is achieved through scopes. Scopes are a mechanism that allows the user to authorize a third-party application to perform only specific operations.

## What Is an ID Token NOT Suitable For?
One of the most common mistakes developers make with an ID token is using it to call an API.

As said above, an ID token proves that a user has been authenticated. In a first-party scenario, i.e. in a scenario where the client and the API are both controlled by you, you may decide that your ID token is good to make authorization decisions: maybe all you need to know is the user identity.

However, even in this scenario, the security of your application, consisting of the client and the API, may be at risk. In fact, there is no mechanism that ties the ID token to the client-API channel. If an attacker manages to steal your ID token, they can use it to call your API like a legitimate client.

For the access token, on the other hand, there is a set of techniques, collectively known as sender constraint, that allow you to bind an access token to a specific sender. This guarantees that even if an attacker steals an access token, they can’t use it to access your API since the token is bound to the client that originally requested it.

In a delegated authorization scenario where a third-party client wants to call your API, you must not use an ID token to call the API. In addition to the lack of mechanisms to bind it to the client, there are several other reasons not to do this.

If your API accepts an ID token as an authorization token, to begin with, you are ignoring the intended recipient stated by the audience claim. That claim says that it is meant for your client application, not for the resource server (i.e., the API).

You may think this is just a formality, but there are security implications here.

First of all, among other validation checks, your API shouldn’t accept a token that is not meant for it. If it does, its security is at risk. In fact, if your API doesn't care if a token is meant for it, an ID token stolen from any client application can be used to access your API. Of course, checking the audience is just one of the checks that your API should do to prevent unauthorized access.

In addition, your ID token will not have granted scopes (I know, this is another pain point). As said before, scopes allow the user to restrict the operations your client application can do on their behalf. Those scopes are associated with the access token so that your API knows what the client application can do and what it can't do. If your client application uses an ID token to call the API, you ignore this feature and potentially allow the application to perform actions that the user has not authorized.

## What Is an Access Token NOT Suitable For?
On the access token side, it was conceived to demonstrate that you are authorized to access a resource, e.g., to call an API.

Your client application should use it only for this reason. In other words, the access token should not be inspected by the client application. It is intended for the resource server, and your client application should treat access tokens as opaque strings, that is, strings with no specific meaning. Even if you know the access token format, you shouldn’t try to interpret its content in your client application. As said, the access token format is an agreement between the authorization server and the resource server, and the client application should not intrude. Think of what can happen if one day the access token format changes. If your client code was inspecting that access token, now it will break unexpectedly.
