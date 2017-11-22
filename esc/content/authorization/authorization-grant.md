## Obtaining Authorization

To request an access token, the client obtains authorization from the
resource owner.  The authorization is expressed in the form of an
authorization grant, which the client uses to request the access
token.  OAuth defines four grant types: 
* authorization code
* implicit
* resource owner password credentials, and 
* client credentials  
It also provides an extension mechanism for defining additional grant types.

Key Bridge ESC implements Implicit grant.

### Authorization Grant
An authorization grant is a credential representing the resource
   owner's authorization (to access its protected resources) used by the
   client to obtain an access token.  This specification defines four
   grant types -- authorization code, implicit, resource owner password
   credentials, and client credentials -- as well as an extensibility
   mechanism for defining additional types.

<!-- 
 1.3.
 4. Obtaining Authorization 
 https://tools.ietf.org/html/rfc6749
 OAUTH 2.0
 -->

####  Implicit Authorization Grant

   The implicit grant is a simplified authorization code flow optimized
   for clients implemented in a browser using a scripting language such
   as JavaScript.  In the implicit flow, instead of issuing the client
   an authorization code, the client is issued an access token directly (as the result of the resource owner authorization).  The grant type
   is implicit, as no intermediate credentials (such as an authorization
   code) are issued (and later used to obtain an access token).

   When issuing an access token during the implicit grant flow, the
   authorization server does not authenticate the client.  In some
   cases, the client identity can be verified via the redirection URI
   used to deliver the access token to the client.  The access token may
   be exposed to the resource owner or other applications with access to
   the resource owner's user-agent.

   Implicit grants improve the responsiveness and efficiency of some
   clients (such as a client implemented as an in-browser application),
   since it reduces the number of round trips required to obtain an
   access token.  

   <!-- However, this convenience should be weighed against
   the security implications of using implicit grants, such as those
   described in Sections 10.3 and 10.16, especially when the
   authorization code grant type is available. -->

