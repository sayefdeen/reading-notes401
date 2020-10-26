# OAuth

## Review, Research, and Discussion

- Why is authentication important?

To make the web application/web site more secure for users.

- Why should we be careful about storing a user’s password?

if anyone can reach the database, or have access on it can see the passwords, or any other related data for any user that's why we have to be more carful when storing the passwords.

- What is the difference between hashing and encryption?

  - Hashing is a one-way function that scrambles plain text to produce a unique message digest

  - Encryption is a two-way function; what is encrypted can be decrypted with the proper key.

- What is the difference between encryption and encoding?

  - Encoding method, data is transformed from one form to another. The main aim of encoding is to transform data into a form that is readable by most of the systems or that can be used by any external process.

  - Encryption in encoding technique in which message is encoded by using encryption algorithm in such a way that only authorized personnel can access the message or information.

* What is a token used for?

The token is used in addition to or in place of a password. It acts like an electronic key to access something.

---

## Vocabulary Terms

- **authentication** : Authentication is the process of recognizing a user’s identity. It is the mechanism of associating an incoming request with a set of identifying credentials. The credentials provided are compared to those on a file in a database of the authorized user’s information on a local operating system or within an authentication server.

- **authorization** : Authorization is a security mechanism to determine access levels or user/client privileges related to system resources including files, services, computer programs, data and application features.

- **encryption** : process that encodes a message or file so that it can be only be read by certain people. Encryption uses an algorithm to scramble, or encrypt, data and then uses a key for the receiving party to unscramble, or decrypt, the information.

- **hashing** : is the transformation of a string of characters into a usually shorter fixed-length value or key that represents the original string.

- **session** :is a temporary and interactive information interchange between two or more communicating devices, or between a computer and user. A session is established at a certain point in time, and then ‘torn down’ - brought to an end - at some later point

* **cookie** : a small piece of data stored on the user's computer by the web browser while browsing a website. Cookies were designed to be a reliable mechanism for websites to remember stateful information or to record the user's browsing activity.

* **token** : is the basic component of source code a user knows, such as a PIN, will enable authorized access to a computer system or network...

* **Basic Auth** : is a method for an HTTP user agent to provide a user name and password when making a request. In basic HTTP authentication.

* **encoding** : is the process of converting data from one form to another.

* **secret** : the secret is a symmetric key that is known by both the sender and the receiver

* **cryptography** : secure information and communication techniques derived from mathematical concepts and a set of rule-based calculations called algorithms, to transform messages in ways that are hard to decipher

---

## Preparation Materials

### OAuth 2 Simplified

- Roles

  - **The Third-Party Application: "Client"** : The client is the application that is attempting to get access to the user's account, It needs to get permission form the user before it can do so.

  - **The API: "Resource Server"** : The resource server is the API server used to access the user's information.

  - **The Authorization Server** : This is the server that presents the interface where the user approves or denies the request

  - **The User: "Resource Owner"** : The resource owner is the person who is giving access to some portion of their account.
