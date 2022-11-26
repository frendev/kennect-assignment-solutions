# JSON Web TOken (JWT)

**JWT** stands for a JSON Web Token. It helps us to securely transfer the information between two parties.

The JWTs can be broken into three parts - Header, Payload, Signature and they are seperated from each other by dot(.)
**Header.Payload.Signature**

1. **Header** - The header contains metadata information about the JSON Web Token. For eg. algorithm - that is, which algorithm has been used to sign the token. And type of the token. In case of JWT it is going to be JWT. Extra headers can also be added depending upon the issuer of the token.
2. **Payload** - It contains claims of the token. A claim is key/value pair where the key is always a string and the value can be any JSON value. Some fields are standard and recommended by the JWT standard. But the most used one's are -

- Issuer `(iss)` - the party that "created" the token and signed it with its private key

- Subject `(sub)` -The entity identified by this token. For example, if the token is used to authorize a user while sending a request to the server, sub could be the user ID.

- Issued At `(iat)` - It is the time at which it was created.

- Expiry `(exp)` - It is the time after which the token will be not usable i.e not acceptable.

  on top of these fields we can add more fields. But these are the recommended ones.

3. **Signature** - The signature is created from the encoded header, encoded payload, a secret (private key) and a the algorithm specified in a header. The signature ensures that the token hasn’t been altered. The party that creates the JWT signs the header and payload with a secret that is known to both the issuer and receiver, or with a private key known only to the sender.

#### The flow of the JWT is as follows -

![JWT Flow](/jwt.png)

Client (Browser) sends post request with credentials to server.
Server authenticates user credential and generates JWT + secret. Server is not storing anything in this case which will save server memory and improve performance.
Sends the JWT on the authorization header.
Sends response to browser.

## Top 3 Benefits -

#### 1. No Database Lookups -

It’s generally known that for most APIs, network calls add the most latency. Hence, it’s reasonable to expect that having no network calls (no database lookups) for session verification is beneficial. JWT is a stateless authentication mechanism as the user state is never saved in the database. As JWTs are self-contained, all the necessary information is there, reducing the need of going back and forward to the database. With JWT we don't need to query database to authenticate the user for every api call. This reduces the latency while using APIs. And also when using Database as a Service (DBaaS) like DynamoDB which charges on the basis of data reads and writes it becomes useful in cost reduction.

#### 2. Authorization -

Once a user is successfully logged in, an application may request to access routes, services, or resources (e.g., APIs) on behalf of that user. To do so, in every request, it must pass an Access Token, which may be in the form of a JWT. Single Sign-on (SSO) widely uses JWT because of the small overhead of the format, and its ability to easily be used across different domains.We can authorize only the requests we wish to authorize.

#### 3. Scalabality -

Since, no user information is stored on the database or on the server. More scalable solutions can be built with a token-based mechanism than the cookie-based method. It can be used in micro-service architecture where in an authorization micro-service can create these tokens. And The rest of your microservices can just have the public key to verify the signature of the tokens. So we can achieve horizontal scalability without synchronizing sessions between servers.
