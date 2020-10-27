# Bearer Authorization

## Review, Research, and Discussion

- Write the following steps in the correct order:

  - Register your application to get a client_id and client_secret
  - Ask the client if they want to sign in via a third party

  - Redirect to a third party authentication endpoint

  - Make a request to the access token endpoint

  - Receive access token

  - Make a request to a third-party API endpoint

  - Receive authorization code

* What can you do with an authorization code?

Send it again to the provider to get the token so the user can be authorized

- What can you do with an access token?

The Token can be saved in the session, cookies , and database so i just can compare with both of them next time the user register

- What’s a benefit of using OAuth instead of your own basic authentication?

More Secure, and for the user it will be more comfortable to use his accounts in Google,LinkedIn, of FaceBook.

---

## Vocabulary Terms

- **Client ID** : It will be generated whenever you register an app in to use as an authenticated app, it can be shared, but it is prefefarable to be in the environment variables

- **Client Secret** : A client secret is a secret known only to your application and the authorization server. It protects your resources by only granting tokens to authorized requestors.

- **Authentication Endpoint** : used to interact with the resource owner and get the authorization to access the protected resource

- **Access Token Endpoint** : Clients obtain identity and access tokens from the token endpoint in exchange for an OAuth 2.0 grant. The grant is a recognised credential which lets the client access the requested resource (web API) or user identity.

- **API Endpoint** : is one end of a communication channel. When an API interacts with another system, the touchpoints of this communication are considered endpoints. For APIs, an endpoint can include a URL of a server or service

- **Authorization Code** : used for any transaction or entry that has restrictions on which users are entitled to access.

- **Access Token** : is an object encapsulating the security identity of a process or thread. A token is used to make security decisions and to store tamper-proof information about some system entity.
