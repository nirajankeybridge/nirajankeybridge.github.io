## Authorization Endpoint

<!-- https://tools.ietf.org/html/rfc6749#section-3.1.2
 -->
The authorization endpoint is used to interact with the resource owner and obtain an authorization grant.  The authorization server MUST first verify the identity of the resource owner. 

``` 
	TO DO:
   The client obtains the location of the authorization endpoint by  ...
```

   The endpoint URI MAY include an ["application/x-www-form-urlencoded"](../urlencoded.md) formatted query component ([[RFC3986] Section 3.4](https://tools.ietf.org/html/rfc3986#section-3.4)),
   which MUST be retained when adding additional query parameters.  The
   endpoint URI MUST NOT include a fragment component.

   Since requests to the authorization endpoint result in user
   authentication and the transmission of clear-text credentials (in the
   HTTP response), the authorization server MUST require the use of TLS
   when sending requests to the authorization endpoint.

The authorization server MUST support the use of the HTTP "GET"
   method [[RFC2616](https://tools.ietf.org/html/rfc2616)] for the authorization endpoint and MAY support the
   use of the "POST" method as well.

Parameters sent without a value MUST be treated as if they were
   omitted from the request.  The authorization server MUST ignore
   unrecognized request parameters.  Request and response parameters
   MUST NOT be included more than once.
