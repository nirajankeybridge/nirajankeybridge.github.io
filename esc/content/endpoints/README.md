# Protocol Endpoints
The authorization process utilizes two authorization server endpoints (HTTP resources):

1. **Authorization endpoint** - used by the client to obtain authorization from the resource owner <!-- via user-agent redirection -->.

<!-- 2. **Token endpoint** - used by the client to exchange an authorization grant for an access token, typically with client authentication. Token
   endpoint is not used for the implicit grant type (since an access token is issued directly). -->

As well as one client endpoint:

2. **Redirection endpoint** - used by the authorization server to return responses containing authorization credentials to the client <!-- via the resource owner user-agent -->.

Not every authorization grant type utilizes both endpoints.    
Extension grant types MAY define additional endpoints as needed.