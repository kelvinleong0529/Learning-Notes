# **Authorization Request Header**
- HTTP authorization request header contains the credential to authenticate a user agent with a server
- APIs uses authorization to ensure client requests access data securely

# **Basic Auth**
- a simple authentication built into the HTTP protocol
- client sends HTTP requests with the Authorization header that contains the word **BASIC**, followed by a space and a base64-encoded (non-encrypted) string username: password
```
Authorization: Basic AXVubzpwQDU1dzByYM==
```
# **Bearer Token / Token Authentication**
- a HTTP authentication scheme that involves security tokens called beared tokens, the token gives access to the bearer of the token
- bearer token is a cryptic string, usually generated by the server in response to a login request
- client must send this token in the Authorization header while requesting to protected resources
```
Authorization: Bearer <token>
```

# **API Key**
- a token that client provides when making API calls
- user sends a key-value pair to the API either in the request headers or query parameters
- Some API use API keys for authorization
```
1. Key in query string
GET /endpoint?api_key=abcdefgh123456789

2. Request header
X-API-Key: abcdefgh123456789
```

# **Digest Auth**
- communicates credentials in an encrypted form by aplying has algorithm to the username and password, the password is converted to response and then sent to the server
- workflow:
1. Client sends a request to the 
2. The server responds with a special code (called a nonce i.e. number used only once), another string representing the realm (a hash) for authentication from the client.
3. The client responds with this nonce and an encrypted version of the username, password, and realm (a hash)
4. If the Client hash matches the server hash, the server will respond with the requested information. Otherwise, it will pass an error message.
```
Authorization: Digest username=”admin” Realm=”abcxyz” nonce=”474754847743646”, uri=”/uri” response=”7cffhfr54685gnnfgerg8”
```

# **OAuth 2.0**
- OAuth 1.0 permits client application to access data provided bu 3rd party API. For example, as a user of a service you can grant another application access to your data with that service without exposing your login details.
- With OAuth 2.0, you first retrieve an access token for the API, then use that token to authenticate future requests. Getting to information via OAuth 2.0 flow varies greatly between API service providers, but typically involves a few requests back and forward between client application, user, and API.
- Workflow:
1. A client application makes a request for the user to authorize access to their data.
2. If the user grants access, the application then requests an access token from the service provider, passing the access grant from the user and authentication details to identify the client.
3. The service provider validates these details and returns an access token.
4. The client uses the access token to request the user data via the service provider.
```
Authorization: Bearer hY_9.B5f-4.1BfE
//where “hY_9.B5f-4.1BfE” is your OAuth Access Token
```

# **Hawk Authentication**
- enables user to authorize requests using partial cryptographic verification
- Hawk Authentication parameters are as follows:
1. Hawk Auth ID: Your API authentication ID value.
2. Hawk Auth Key: Your API authentication key value.
3. Algorithm: The hash algorithm(sha266, sha1) used to create the message authentication code(MAC).
```
Authorization: Hawk id="abcxyz123", ts="1592459563", nonce="gWqbkw", mac="vxBCccCutXGV30gwEDKu1NDXSeqwfq7Z0sg/HP1HjOU="
```

# **AWS Signature**
- AWS is the authorization workflow for Amazon Web Services requests. AWS uses a custom HTTP scheme based on a keyed-HMAC (Hash Message Authentication Code) for authentication.
- AWS Authentication Parameters are as follows:
1. Access Key: API Access key value.
2. Secret Key: API Secret key value.
- Developers are issued an AWS access key ID and AWS secret access key when they register. For request authentication, the AWSAccessKeyId element identifies the access key ID that was used to compute the signature and, indirectly, the developer making the request.
```
Authorization: AWS4-HMAC-SHA256 Credential=abc/20200618/us-east-1/execute-api/aws4_request, SignedHeaders=host;x-amz-date, Signature=c6c85d0eb7b56076609570f4dbdf730d0a017208d964c615253924149ce65de5
```