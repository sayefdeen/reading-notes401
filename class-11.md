# Authentication

## Review, Research, and Discussion

- Explain what a “Singleton” is (in Computer Science terms)

The singleton pattern is a software design pattern that restricts the instantiation of a class to one "single" instance. This is useful when exactly one object is needed to coordinate actions across the system

- Explain how the Singleton pattern can be used with Node modules, specifically with classes.

When you want to use `model.exports` to export a class for an example we usually use the following code .

```javascript
class Test {
  constructor() {}

  method1() {}
  method2() {}
  method3() {}
}
module.exports = Test;
```

To make it a Singleton pattern you have to exports a new instance of the class, even if you require it in multiple files it will always point to the same Class

```javascript
Class Test {
    constructor(){}

    method1(){}
    method2(){}
    method3(){}
}
module.exports = new Test()
}
```

- If you were tasked with building a middleware system like Express uses, what approach might you take to construct/operate it?

---

## Vocabulary Terms

- **Router Middleware** : Router level middleware works the same as application-level middleware, but it calls an instance of `express.Router()`, and it uses `route.method()` or `route, in general routes middleware work when one of the routes has been called or a specifics route was called.

- **Dynamic Module Loading** :

* **Singleton Pattern** : The singleton pattern is a design pattern that restricts the instantiation of a class to one object.

* **CRUD -> REST Method Matches** :

  - CRUD : Create Read Update Delete
  - Rest : POST GET PUT/PITCH DELETE

* **Mock Testing** : is an approach to unit testing that lets you make assertions about how the code under test is interacting with other system modules. In mock testing, the dependencies are replaced with objects that simulate the behavior of the real ones.

---

## Preparation Materials

Passwords are the first line of defense against cyber criminals, so storing passwords into data base in a wrong action, anyone can access the data base can see passwords as a plain text.

Hashing is the greatest way for protecting passwords and considered to be pretty safe for ensuring the integrity of data or password.

The main benefit of hashing is that id someone steals the database with hashed passwords, they only make off with hashes and not the actual plaintext passwords, in some cases we hear that the passwords was cracked why is that? there is some weakness in cryptographic hash algorithm that allows an attacker to calculate the original value of a hashed password.

Problems with cryptographic hash algorithm :

- **Brute Force attack**: Hashes can't be reversed, so instead of reversing the hash of the password, an attacker can simply keep trying different inputs until he does not find the right now that generates the same hash value, called brute force attack.

- **Hash Collision attack**: Hash functions have infinite input length and a predefined output length, so there is inevitably going to be the possibility of two different inputs that produce the same output hash. MD5, SHA1, SHA2 are vulnerable to Hash Collision Attack i.e. two input strings of a hash function that produce the same hash result.

### BCrypt, IT's SLOW AND STRONG

To overcome such issues, we need algorithms which can make the brute force attacks slower and minimize the impact, Such algorithms are [PBKDF2](https://nodejs.org/api/crypto.html#crypto_crypto_pbkdf2_password_salt_iterations_keylen_digest_callback) and [BCrypt](https://www.npmjs.com/package/bcrypt).

---
