## Response Type

   The authorization endpoint is used by the authorization code grant
   type and implicit grant type flows. Key Bridge ESC uses the Implicit grant type flow.  

   The client informs the authorization server of the desired grant type using the following parameter:
```
   response_type  REQUIRED.    
```
   The value MUST be "token" for requesting an access token (implicit
         grant) as described by [Implicit Flow Authorization Request](../authorization/authorization-implicit-request.html).
         
   Extension response types MAY contain a space-delimited (%x20) list of
   values, where the order of values does not matter (e.g., response
   type `a b` is the same as `b a`).  The meaning of such composite
   response types is defined by their respective specifications.

   If an authorization request is missing the "response_type" parameter,
   or if the response type is not understood, the authorization server
   MUST return an [error response](../authorization/authorization-implicit-response-error.html)