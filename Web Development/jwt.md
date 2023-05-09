# **JSON Web Tokens**
- `JSON web tokens (JWT)` is an open stnadard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object
- this information can be verified and trusted because it is digitally signed using a secret (with HMAC) or a public/private key pair using RSA or ECDSA

# **Why use JSON Web Tokens**

## **Authorization**
- once user is logged in, each subsequent request will include JWTm allowing user to access routes, services, and resources that are permitted with that token
- `Single Sign On` is a featrure that widely uses JWT nowadays, because of its small overhead and its ability to be easily used accross different domains

## **Information Exchange**
- JWT are a good way to securely transmitting information between parties
- since JWT can be signed, we can validate the senders; additionally the signature is calculated using the header and the payload, we can also verify that the content hasn't been tampered with

# **JWT Structure**
- JWT usually consists of 3 parts separated by dots, which are:
1. Header
2. Payload
3. Signature

## **Header**
- `header` typically consists of 2 parts: the type of the token, which is `JWT`, and the signing algorithm being used, such as HMAC SHA256 or RSA
```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

## **Payload**
- payload contains the claim, which are statements anout an entity (typically the user) and additional data
- there are 3 types of claims: registered, public and private
### **1. Registered Claim**
- there are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims
- some of them are: **iss**(issuer), **exp**(expiration time), **sub**(subject), **aud**(audience), and others

### **2. Public Claim**
- These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace

### **3. Private Claim**
- These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

## **Signature**
- to create signature part we have to take the encoded header, encoded payload, a secret, algorithm specified in the header, and sign that
- The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

# **How do JWT work**
- in authentication, when the user successfully logs in using their credentials, a JWT will be returned
- whenver the user wants to access a protected route or resource, the user agent should sent the JWT, typically in the `Authorization` header using the `Bearer` schema, as below:
```
Authorization: Bearer <token>
```
- This can be, in certain cases, a stateless authorization mechanism. The server's protected routes will check for a valid JWT in the Authorization header, and if it's present, the user will be allowed to access protected resources
- If the JWT contains the necessary data, the need to query the database for certain operations may be reduced, though this may not always be the case