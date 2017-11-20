# Implicit Flow - Error Response


<!-- 
 Section 4.2.2. Access Token Response
 https://tools.ietf.org/html/rfc6749
 OAUTH 2.0
 -->

 If the request fails due to a missing, invalid, or mismatching
   redirection URI, or if the client identifier is missing or invalid,
   the authorization server SHOULD inform the resource owner of the
   error and MUST NOT automatically redirect the user-agent to the
   invalid redirection URI.

   If the resource owner denies the access request or if the request
   fails for reasons other than a missing or invalid redirection URI,
   the authorization server informs the client by adding the following
   parameters to the fragment component of the redirection URI using the
   ["application/x-www-form-urlencoded"](../../content/urlencoded.md) format:

|FIELD NAME| R/O/C | DESCRIPTION | 
|---|---|---|
| error| REQUIRED | A single ASCII [USASCII] error code from the Error Codes list below. <br/>Values for the "error" parameter MUST NOT include characters outside the set %x20-21 / %x23-5B / %x5D-7E.|
|error_description | OPTIONAL | Human-readable ASCII [USASCII] text providing additional information, used to assist the client developer in understanding the error that occurred. <br/>Values for the "error_description" parameter MUST NOT include characters outside the set %x20-21 / %x23-5B / %x5D-7E.|
| error_uri | OPTIONAL |  A URI identifying a human-readable web page with information about the error, used to provide the client developer with additional information about the error. <br/>Values for the "error_uri" parameter MUST conform to the URI-reference syntax and thus MUST NOT include characters outside the set %x21 / %x23-5B / %x5D-7E. | 
| state | REQUIRED | if a "state" parameter was present in the client authorization request.  The exact value received from the client. | 

#### List Of Error Codes 
```
invalid_request
      The request is missing a required parameter, includes an
      invalid parameter value, includes a parameter more than
      once, or is otherwise malformed.
      
unauthorized_client
      The client is not authorized to request an access token
      using this method.

access_denied
      The resource owner or authorization server denied the
      request.

unsupported_response_type
      The authorization server does not support obtaining an
      access token using this method.

invalid_scope
      The requested scope is invalid, unknown, or malformed.

server_error
      The authorization server encountered an unexpected
      condition that prevented it from fulfilling the request.
      (This error code is needed because a 500 Internal Server
      Error HTTP status code cannot be returned to the client
      via an HTTP redirect.)

temporarily_unavailable
      The authorization server is currently unable to handle
      the request due to a temporary overloading or maintenance
      of the server.  (This error code is needed because a 503
      Service Unavailable HTTP status code cannot be returned
      to the client via an HTTP redirect.)

```

   For example, the authorization server redirects the user-agent by
   sending the following HTTP response:
```
   HTTP/1.1 302 Found
   Location: https://client.example.com/cb#error=access_denied&state=xyz
```