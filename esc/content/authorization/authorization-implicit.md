# Implicit Flow - Authorization


<!-- 
![](/assets/dpa-state-diagram.svg)

**Figure 2: DPA State Machine in a channel per DPA**
 1.2. Protocol Flow 
 https://tools.ietf.org/html/rfc6749
 OAUTH 2.0
 -->
 
 The implicit grant type is used to obtain access tokens (it does not support the issuance of refresh tokens) and is optimized for public clients known to operate a particular redirection URI.  These clients are typically implemented in a browser using a scripting language such as JavaScript.

 Since this is a redirection-based flow, the client must be capable of interacting with the resource owner's user-agent (typically a web browser) and capable of receiving incoming requests (via redirection) from the authorization server.
 
 Unlike the authorization code grant type, in which the client makes separate requests for authorization and for an access token, the client receives the access token as the result of the authorization request.
 
 The implicit grant type does not include client authentication, and relies on the presence of the resource owner and the registration of the redirection URI.  Because the access token is encoded into the redirection URI, it may be exposed to the resource owner and other applications residing on the same device.

![](..\..\assets\implicit-flow.svg)<br/>Figure 4: *Implicit Grant Flow*

Note: The lines illustrating steps (A) and (B) are broken into two
parts as they pass through the user-agent.

Based on [RFC 6749](https://tools.ietf.org/html/rfc6749), the flow illustrated in Figure 4 includes the following steps:

   **(A)**  The SAS client initiates the flow by directing the ESC Operator's
        user-agent to the authorization endpoint.  The SAS includes
        its SAS client identifier, requested scope, local state, and a
        redirection URI to which the authorization server will send the
        user-agent back once access is granted (or denied).

   **(B)**  The authorization server authenticates the ESC Operator (via
        the user-agent) and establishes whether the ESC Operator
        grants or denies the client's access request.

   **(C)**  Assuming the ESC Operator grants access, the authorization
        server redirects the user-agent back to the SAS client using the
        redirection URI provided earlier.  The redirection URI includes
        the access token in the URI fragment.

   **(D)**  The user-agent follows the redirection instructions by making a
        request to the web-hosted client resource (which does not
        include the fragment per [[RFC2616](https://tools.ietf.org/html/rfc2616)]).  The user-agent retains the
        fragment information locally.

   **(E)**  The web-hosted client resource returns a web page (typically an
        HTML document with an embedded script) capable of accessing the
        full redirection URI including the fragment retained by the
        user-agent, and extracting the access token (and other
        parameters) contained in the fragment.

   **(F)**  The user-agent executes the script provided by the web-hosted
        client resource locally, which extracts the access token.

   **(G)**  The user-agent passes the access token to the SAS client.

<!--    See Sections 1.3.2 and 9 for background on using the implicit grant.
   See Sections 10.3 and 10.16 for important security considerations
   when using the implicit grant. -->