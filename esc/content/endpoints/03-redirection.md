## Redirection Endpoint

   After completing its interaction with the resource owner, the
   authorization server directs the resource owner's user-agent back to
   the client.  The authorization server redirects the user-agent to the
   client's redirection endpoint previously established with the
   authorization server during the client registration process or when
   making the authorization request.

   The redirection endpoint URI MUST be an absolute URI as defined by
   [[RFC3986] Section 4.3](https://tools.ietf.org/html/rfc3986#section-4.3).  The endpoint URI MAY include an
   ["application/x-www-form-urlencoded"](../../content/endpoints/urlencoded.md) query
   component [([RFC3986] Section 3.4)](https://tools.ietf.org/html/rfc3986#section-3.4), which MUST be retained when adding
   additional query parameters.  The endpoint URI MUST NOT include a
   fragment component.

### Endpoint Request Confidentiality

   The redirection endpoint SHOULD require the use of TLS as described
   in Section 1.6 when the requested response type is "code" or "token",
   or when the redirection request will result in the transmission of
   sensitive credentials over an open network.  This specification does
   not mandate the use of TLS because at the time of this writing,
   requiring clients to deploy TLS is a significant hurdle for many
   client developers.  If TLS is not available, the authorization server
   SHOULD warn the resource owner about the insecure endpoint prior to
   redirection (e.g., display a message during the authorization
   request).

   Lack of transport-layer security can have a severe impact on the
   security of the client and the protected resources it is authorized
   to access.  The use of transport-layer security is particularly
   critical when the authorization process is used as a form of
   delegated end-user authentication by the client (e.g., third-party
   sign-in service).

### Registration Requirements

   The authorization server MUST require the following clients to
   register their redirection endpoint:

   * Public clients.

   * Confidential clients utilizing the implicit grant type.

   The authorization server SHOULD require all clients to register their
   redirection endpoint prior to utilizing the authorization endpoint.

   The authorization server SHOULD require the client to provide the
   complete redirection URI (the client MAY use the "state" request
   parameter to achieve per-request customization).  If requiring the
   registration of the complete redirection URI is not possible, the
   authorization server SHOULD require the registration of the URI
   scheme, authority, and path (allowing the client to dynamically vary
   only the query component of the redirection URI when requesting
   authorization).

   The authorization server MAY allow the client to register multiple
   redirection endpoints.

   Lack of a redirection URI registration requirement can enable an
   attacker to use the authorization endpoint as an open redirector. 
   <!-- as described in Section 10.15. -->

#### Open Redirectors (Security Consideration)

   The authorization server, authorization endpoint, and client
   redirection endpoint can be improperly configured and operate as open
   redirectors.  An open redirector is an endpoint using a parameter to
   automatically redirect a user-agent to the location specified by the
   parameter value without any validation.

   Open redirectors can be used in phishing attacks, or by an attacker
   to get end-users to visit malicious sites by using the URI authority
   component of a familiar and trusted destination.  In addition, if the
   authorization server allows the client to register only part of the
   redirection URI, an attacker can use an open redirector operated by the client to construct a redirection URI that will pass the
   authorization server validation but will send the authorization code
   or access token to an endpoint under the control of the attacker.

### Dynamic Configuration

   If multiple redirection URIs have been registered, if only part of
   the redirection URI has been registered, or if no redirection URI has
   been registered, the client MUST include a redirection URI with the
   authorization request using the "redirect_uri" request parameter.

   When a redirection URI is included in an authorization request, the
   authorization server MUST compare and match the value received
   against at least one of the registered redirection URIs (or URI
   components) as defined in [[RFC3986] Section 6](https://tools.ietf.org/html/rfc3986#section-6), if any redirection
   URIs were registered.  If the client registration included the full
   redirection URI, the authorization server MUST compare the two URIs
   using simple string comparison as defined in [[RFC3986] Section 6.2.1](https://tools.ietf.org/html/rfc3986#section-6.2.1).

### Invalid Endpoint

   If an authorization request fails validation due to a missing,
   invalid, or mismatching redirection URI, the authorization server
   SHOULD inform the resource owner of the error and MUST NOT
   automatically redirect the user-agent to the invalid redirection URI.

### Endpoint Content

   The redirection request to the client's endpoint typically results in
   an HTML document response, processed by the user-agent.  If the HTML
   response is served directly as the result of the redirection request,
   any script included in the HTML document will execute with full
   access to the redirection URI and the credentials it contains.

   The client SHOULD NOT include any third-party scripts (e.g., third-
   party analytics, social plug-ins, ad networks) in the redirection
   endpoint response.  Instead, it SHOULD extract the credentials from
   the URI and redirect the user-agent again to another endpoint without
   exposing the credentials (in the URI or elsewhere).  If third-party
   scripts are included, the client MUST ensure that its own scripts
   (used to extract and remove the credentials from the URI) will
   execute first.