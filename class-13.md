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

---

## Preparation Materials

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed.

### What is the JSON Web Token structure?

- Header : The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Then, this JSON is Base64Url encoded to form the first part of the JWT.

- Payload : The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data.

  - Registered claims: These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims.

  - Public claims: These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.

  - Private claims: These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

- Signature: To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

```javascript
HMACSHA256(base64UrlEncode(header) + '.' + base64UrlEncode(payload), secret);
```

The Final result would look like something like this.

![Final Result](https://cdn.auth0.com/content/jwt/encoded-jwt3.png)

JWTs can be either signed, encrypted or both. If a token is signed, but not encrypted, everyone can read its contents, but when you don't know the private key, you can't change it. Otherwise, the receiver will notice that the signature won't match anymore.

JWT doesn't concern itself with encryption. It cares about validation. That is to say, it can always get the answer for "Have the contents of this token manipulated"? This means user manipulation of the JWT token is futile because the server will know and disregard the token. The server adds a signature based on the payload when issuing a token to the client. Later on it verifies the payload and matching signature.
