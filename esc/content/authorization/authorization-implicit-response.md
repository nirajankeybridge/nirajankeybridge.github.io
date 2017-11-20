# Implicit Flow - Access Token Response


<!-- 
 Section 4.2.2. Access Token Response
 https://tools.ietf.org/html/rfc6749
 OAUTH 2.0
 -->

   If the resource owner grants the access request, the authorization
   server issues an access token and delivers it to the client by adding
   the following parameters to the fragment component of the redirection
   URI using the "application/x-www-form-urlencoded" format, per
   Appendix B:

|FIELD NAME| R/O/C | DESCRIPTION | 
|---|---|---|
|access_token | REQUIRED |  The access token issued by the authorization server. |
|token_type | REQUIRED |  The type of the token issued as described [below](#Access-Token-Types). Value is case insensitive. |
| expires_in | RECOMMENDED|  The lifetime in seconds of the access token.  For example, the value "3600" denotes that the access token will expire in one hour from the time the response was generated. If omitted, the authorization server SHOULD provide the expiration time via other means or document the default value. |
|scope | OPTIONAL if identical to the scope requested by the client; otherwise, REQUIRED |   The scope of the access token as described by Section ["Action Token Scope"](../endpoints/04-scope.md)|
|state | REQUIRED if the "state" parameter was present in the client authorization request. |  The exact value received from the client. |

   The authorization server MUST NOT issue a refresh token.

   For example, the authorization server redirects the user-agent by
   sending the following HTTP response (with extra line breaks for
   display purposes only):

```
     HTTP/1.1 302 Found
     Location: http://example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA
               &state=xyz&token_type=example&expires_in=3600
```

   Developers should note that some user-agents do not support the
   inclusion of a fragment component in the HTTP "Location" response
   header field.  Such clients will require using other methods for
   redirecting the client than a 3xx redirection response -- for
   example, returning an HTML page that includes a 'continue' button
   with an action linked to the redirection URI.

   The client MUST ignore unrecognized response parameters. The access token string size is left undefined by this specification. The client should avoid making assumptions about value sizes. The authorization server SHOULD document the size of any value it issues.

## Access Token Types
<!-- https://tools.ietf.org/html/rfc6749#section-7.1 -->
The access token type provides the client with the information
   required to successfully utilize the access token to make a protected
   resource request (along with type-specific attributes).  The client
   MUST NOT use an access token if it does not understand the token
   type.

   For example, the "bearer" token type defined in [[RFC6750]](https://tools.ietf.org/html/rfc6750) is utilized
   by simply including the access token string in the request:
```
     GET /resource/1 HTTP/1.1
     Host: example.com
     Authorization: Bearer mF_9.B5f-4.1JqM
```
   while the "mac" token type defined in [[OAuth-HTTP-MAC]](https://tools.ietf.org/html/rfc6749#ref-OAuth-HTTP-MAC) is utilized by
   issuing a Message Authentication Code (MAC) key together with the
   access token that is used to sign certain components of the HTTP
   requests:
```
     GET /resource/1 HTTP/1.1
     Host: example.com
     Authorization: MAC id="h480djs93hd8",
                        nonce="274312:dj83hs9s",
                        mac="kDZvddkndxvhGRXZhvuDjEWhGeE="
```
   The above examples are provided for illustration purposes only.
   Developers are advised to consult the [[RFC6750]](https://tools.ietf.org/html/rfc6750) and [[OAuth-HTTP-MAC]](https://tools.ietf.org/html/rfc6749#ref-OAuth-HTTP-MAC)
   specifications before use.

   Each access token type definition specifies the additional attributes
   (if any) sent to the client together with the "access_token" response
   parameter.  It also defines the HTTP authentication method used to
   include the access token when making a protected resource request.