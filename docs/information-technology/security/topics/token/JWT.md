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

## Application areas

### Authorization/Authentication

- Once the user is logged in, you give a JWT to the user which is kept in the user's browser's cache/local storage/cookie etc. Then each subsequent request that is made to the application/server bears this token, it is included in each request, where it is validated to make sure user is who they claim to be and are logged in.
- SSO structures usually employ JWT

### Data transmission

- Between two parties
- Signing helps with identifying the other party, and making sure they are who they claim to be
- Header and signature is used for verifying the contents of the payload against any tempering and alteration during the transfer


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
