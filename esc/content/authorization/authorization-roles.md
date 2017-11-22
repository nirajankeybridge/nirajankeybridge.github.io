## Roles

OAuth defines four roles:

### 1. Resource Owner (ESC Operator):
>An entity capable of granting access to a protected resource. When the resource owner is a person, it is referred to as an end-user.

### 2. Resource Server (ESC Server): 
>The server hosting the protected resources, capable of accepting and responding to protected resource requests using access tokens.

### 3. Client (SAS):
>An application making protected resource requests on behalf of the resource owner and with its authorization.  The term "client" does not imply any particular implementation characteristics (e.g., whether the application executes on a server, a desktop, or other devices).

### 4. Authorization Server:
> The server issuing access tokens to the client after successfully authenticating the resource owner and obtaining authorization.
The authorization server may be the same server as the resource server or a separate entity.

Additionally, in the context of Implicit flow, user agent is also involved:
### 5. User Agent: 
> The agent used by the Resource Owner to interact with the Client, for example a browser or a native application.
