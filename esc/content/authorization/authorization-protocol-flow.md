# Abstract OAuth 2.0 Protocol Flow


<!-- 
 1.2. Protocol Flow
 4. Obtaining Authorization 
 https://tools.ietf.org/html/rfc6749
 OAUTH 2.0
 -->



![](..\..\assets\abstract-oauth-flow.svg)<br/>Figure 1: *Abstract Protocol Flow*

Based on [RFC 6749](https://tools.ietf.org/html/rfc6749), the abstract OAuth 2.0 flow illustrated in Figure 1 describes the interaction between the four roles and includes the following steps:

* (A)  The SAS requests authorization from the ESC Operator.  The authorization request can be made directly to the ESC Operator (as shown), or preferably indirectly via the authorization server as an intermediary.

* (B)  The SAS receives an authorization grant, which is a credential representing the ESC Operator's authorization, expressed using one of four grant types defined in this specification or using an extension grant type.  The authorization grant type depends on the method used by the SAS to request authorization and the types supported by the authorization server.

* (C)  The SAS requests an access token by authenticating with the authorization server and presenting the authorization grant.

* (D)  The authorization server authenticates the SAS and validates the authorization grant, and if valid, issues an access token.

* (E)  The SAS requests the protected resource from the resource server and authenticates by presenting the access token.

* (F)  The ESC server validates the access token, and if valid, serves the request.

The preferred method for the SAS to obtain an authorization grant from the ESC Operator (depicted in steps (A) and (B)) is to use the authorization server as an intermediary, which is illustrated in the figure below. 