# Implicit Flow - Authorization Request


<!-- 
 44.2.1. Implicit Authorization Request 
 https://tools.ietf.org/html/rfc6749
 OAUTH 2.0
 -->
 
The client constructs the request URI by adding the following
parameters to the query component of the authorization endpoint URI
using the ["application/x-www-form-urlencoded"](urlencoded.md) format:

|FIELD NAME| R/O/C | DESCRIPTION | 
|---|---|---|
|response_type|REQUIRED|  Value MUST be set to "token".|
|client_id | REQUIRED|The client identifier |
| redirect_uri | OPTIONAL | As described in Section [Redirection Endpoint](../content/endpoints/03-redirection.md)| 
| scope | OPTIONAL | The scope of the access request as described by Section [Access Token Scope](../content/endpoints/04-scope.md)|
| state | RECOMMENDED | An opaque value used by the client to maintain state between the request and callback.  The authorization server includes this value when redirecting the user-agent back to the client.  The parameter SHOULD be used for preventing [cross-site request forgery](../content/security.md#cross-site) as described in Security Considerations|  
 

The client directs the resource owner to the constructed URI using an
HTTP redirection response, or by other means available to it via the
user-agent.

For example, the client directs the user-agent to make the following
HTTP request using TLS (with extra line breaks for display purposes
only):

```
GET /authorize?response_type=token&client_id=s6BhdRkqt3&state=xyz
    &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
Host: server.example.com
```

The authorization server validates the request to ensure that all
required parameters are present and valid.  The authorization server
MUST verify that the redirection URI to which it will redirect the
access token matches a redirection URI registered by the client as
described in [Redirection Endpoint](../content/endpoints/03-redirection.md).

If the request is valid, the authorization server authenticates the
resource owner and obtains an authorization decision (by asking the
resource owner or by establishing approval via other means).

When a decision is established, the authorization server directs the
user-agent to the provided client redirection URI using an HTTP
redirection response, or by other means available to it via the
user-agent.