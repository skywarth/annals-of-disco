# JWT

> JSON Web Token


- [RFC 7519](https://tools.ietf.org/html/rfc7519)
- Used for securely transmitting JSON data between two parties
- It incorporates signing and verification mechanisms
- JWTs can be signed by:
	- A secret key, using HMAC
	- Public/private key pair like in any asymmetric cryptography algorithm
		- RSA
		- ECDSA
- **JWT doesn't offer data privacy. Anyone and everyone can read and parse the data transmitted, no matter the algorithm nor the secret for signature.**
	- If you ever need to send sensitive information in the JWT payload, make sure it is encrypted
	- Assume that everyone will see the contents of the payload

## Application areas

### Authorization/Authentication

- Once the user is logged in, you give a JWT to the user which is kept in the user's browser's cache/local storage/cookie etc. Then each subsequent request that is made to the application/server bears this token, it is included in each request, where it is validated to make sure user is who they claim to be and are logged in.
- SSO structures usually employ JWT

### Data transmission

- Between two parties
- Signing helps with identifying the other party, and making sure they are who they claim to be
- Header and signature is used for verifying the contents of the payload against any tempering and alteration during the transfer

## Structure

Consisting of three parts:
- [[#Header]]
- Payload
- Signature

- Each part is separated by `.`, example: `xxxxx.yyyyy.zzzzz`

### Header

Usually consists of two parts:
- Token type: `JWT`
- And the signing algorithm being used for this token. E.g: `SHA256`, `RSA`, `HMAC`

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Above is the JSON format of it, it is later encoded with Base64Url to be turned into a stream of string, so it can be used in the first part of the string.

### Payload

The actual payload, the data you want to transmit. It contains **claims**. In JWT, **claims** are statements about the entity in question, usually this is the user. 

There are three types of claims:
- Registered: Standard, recommended for interoperability
- Public: [IANA JSON Web Token Registry](https://www.iana.org/assignments/jwt/jwt.xhtml)
- Private: custom data

Payload is JSON, and is also encoded with Base64Url to be converted into a line string

### Signature

Last section of the encoded JWT token string. 

Signature is created by merging the encoded header and payload, joining them with `.` as usual, then you need a secret (private), and need to choose a encryption algorithm. Then you sign it with that algorithm.

Since the receiver can easily decode the header section (after verifying the JWT structure, which is recommended), the receiver knows which algorithm is used for the signing process. This way it can be verified.

## Resources

- https://jwt.io/introduction
- https://www.youtube.com/watch?v=fyTxwIa-1U0 (Hey I remember this guy from HLD/LLD tutorial!)
- https://dev.to/jaypmedia/jwt-explained-in-4-minutes-with-visuals-g3n
- https://supertokens.com/blog/what-is-jwt
- https://arielweinberger.medium.com/json-web-token-jwt-the-only-explanation-youll-ever-need-cf53f0822f50
- https://www.reddit.com/r/learnjavascript/comments/u450is/can_anybody_explain_jwt_in_simplified_way_because/
- https://fusionauth.io/articles/tokens/jwt-components-explained
- https://en.wikipedia.org/wiki/JSON_Web_Token
- https://www.ibm.com/docs/en/cics-ts/6.x?topic=cics-json-web-token-jwt
