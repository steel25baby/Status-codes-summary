# HTTP response status codes  
HTTP response status codes indicate whether a specific HTTP request has been successfully completed. Responses are grouped in five classes:  
1. Informational responses (100 – 199)  
2. Successful responses (200 – 299)
3. Redirection messages (300 – 399)
4. Client error responses (400 – 499)
5. Server error responses (500 – 599)  


## Information responses  
#### 100 Continue  
 - Indicates that everything so far is OK and that the client should continue with the request or ignore it if it is already finished.  
 - To have a server check the request's headers, a client must send _Expect: 100-continue_ as a header in its initial request and receive a 100 Continue status code in response before sending the body.  

 #### 101 Switching Protocols  
 -  Indicates a protocol to which the server switches. The protocol is specified in the Upgrade request header received from a client.  
 - The server includes in this response an _Upgrade_ response header to indicate the protocol it switched to.  

 #### 102 Processing  
 -  Indicates to client that a full request has been received and the server is working on it.  
 -  Sent if the server expects the request to take significant time. It tells the client that your request is not dead yet.    

 Note: This status code is deprecated.Clients may still accept it, but simply ignore them.  

 #### 103 Early Hints  
 - Sent by a server while it is still preparing a response, with hints about the sites and resources that the server is expecting the final response will link. This allows a browser to __preconnect__ to sites or start __preloading__ resources even before the server has prepared and sent that final response.  
 - The early hint response is primarily intended for use with the _Link_ header, which indicates the resources to be loaded.  

 Note: For compatibility reasons it is recommended to only send HTTP 103 Early Hints responses over HTTP/2 or later, unless the client is known to handle informational responses correctly.  

 ## Successful responses  
 #### 200 OK
 Indicates that the request has succeeded. A 200 response is cacheable by default.  
 The meaning of a success depends on the HTTP request method:  
 - GET: The resource has been fetched and is transmitted in the message body.
- HEAD: The representation headers are included in the response without any message body
- POST: The resource describing the result of the action is transmitted in the message body
- TRACE: The message body contains the request message as received by the server.  
#### 201 Created
- Indicates that the request has succeeded and has led to the creation of a resource. The new resource, or a description and link to the new resource, is effectively created before the response is sent back and the newly created items are returned in the body of the message, located at either the URL of the request, or at the URL in the value of the _Location_ header.  
-The common use case of this status code is as the result of a POST request.  
#### 202 Accepted  
- Indicates that the request has been accepted for processing, but the processing has not been completed; in fact, processing may not have started yet. The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place.  
- It is non-committal, meaning that there is no way for the HTTP to later send an asynchronous response indicating the outcome of processing the request. It is intended for cases where another process or server handles the request, or for batch processing.  
#### 203 Non-Authoritative Information   
- Indicates that the request was successful but the enclosed payload has been modified by a transforming _proxy_ from that of the origin server's 200 (OK) response.   
#### 204 No Content  
-  Indicates that a request has succeeded, but that the client doesn't need to navigate away from its current page.  
#### 205 Reset Content  
- Tells the client to reset the document view, so for example to clear the content of a form, reset a canvas state, or to refresh the UI.  
#### 206 Partial Content  
- Indicates that the request has succeeded and the body contains the requested ranges of data, as described in the _Range_ header of the request.  
- If there is only one range, the _Content-Type_ of the whole response is set to the type of the document, and a _Content-Range_ is provided.  
#### 207 Multi-Status  
 - Indicates that there might be a mixture of responses.  
 - The response body is a text/xml or application/xml HTTP entity with a multistatus root element. The XML body will list all individual response codes.  
 #### 208 Already Reported  
 - Used in a 207 (207 Multi-Status) response to save space and avoid conflicts.  
 - Responses for all other bindings will report with this 208 status code, so no conflicts are created and the response stays shorter.   
 #### 226 IM Used  
 -  St by the server to indicate that it is returning a delta to the GET request that it received.  
 - IM stands for __instance manipulations__ the term used to describe an algorithm generating a delta.  

 ## Redirection messages  
  
  #### 300 Multiple Choices  
  - indicates that the request has more than one possible response. The user-agent or the user should choose one of them. As there is no standardized way of choosing one of the responses, this response code is very rarely used.  
  - If the server has a preferred choice, it should generate a Location header.  
  #### 301 Moved Permanently  
 - Indicates that the requested resource has been definitively moved to the URL given by the Location headers. A browser redirects to the new URL and search engines update their links to the resource.   

 Note: Although the specification requires the method and the body to remain unchanged when the redirection is performed, not all user-agents meet this requirement.  

 #### 302 Found  
 - indicates that the resource requested has been temporarily moved to the URL given by the Location header. A browser redirects to this page but search engines don't update their links to the resource (in 'SEO-speak', it is said that the 'link-juice' is not sent to the new URL).  
 - Even if the specification requires the method (and the body) not to be altered when the redirection is performed, not all user-agents conform here - you can still find this type of bugged software out there.  
 #### 303 See Other  
 -  Indicates that the redirects don't link to the requested resource itself, but to another page (such as a confirmation page, a representation of a real-world object — see HTTP range-14 — or an upload-progress page). This response code is often sent back as a result of PUT or POST. The method used to display this redirected page is always GET.  

 #### 304 Not Modified  
 - Indicates that there is no need to retransmit the requested resources. This response code is sent when the request is a conditional GET or HEAD request with an If-None-Match or an If-Modified-Since header and the condition evaluates to false. It is an implicit redirection to a cached resource that would have resulted in a 200 OK response if the condition evaluated to true.  
 #### 307 Temporary Redirect  
 - Indicates that the resource requested has been temporarily moved to the URL given by the _Location_ headers.  
 - The method and the body of the original request are reused to perform the redirected request.  
 #### 308 Permanent Redirect  
 - Indicates that the resource requested has been definitively moved to the URL given by the _Location_ headers. A browser redirects to this page and search engines update their links to the resource (in 'SEO-speak', it is said that the 'link-juice' is sent to the new URL).  

 ## Client error responses  
 #### 400 Bad Request
- The server cannot or will not process the request due to something that is perceived to be a client error (e.g., malformed request syntax, invalid request message framing, or deceptive request routing).  
#### 401 Unauthorized
- Although the HTTP standard specifies "unauthorized", semantically this response means "unauthenticated". That is, the client must authenticate itself to get the requested response.  
#### 403 Forbidden
- The client does not have access rights to the content; that is, it is unauthorized, so the server is refusing to give the requested resource. Unlike 401 Unauthorized, the client's identity is known to the server.  
#### 404 Not Found
- The server cannot find the requested resource. In the browser, this means the URL is not recognized. In an API, this can also mean that the endpoint is valid but the resource itself does not exist. Servers may also send this response instead of 403 Forbidden to hide the existence of a resource from an unauthorized client. This response code is probably the most well known due to its frequent occurrence on the web.  
#### 405 Method Not Allowed
- The request method is known by the server but is not supported by the target resource. For example, an API may not allow calling DELETE to remove a resource.  
#### 406 Not Acceptable
- This response is sent when the web server, after performing server-driven content negotiation, doesn't find any content that conforms to the criteria given by the user agent.

#### 407 Proxy Authentication Required
- This is similar to 401 Unauthorized but authentication is needed to be done by a proxy.

#### 408 Request Timeout
- This response is sent on an idle connection by some servers, even without any previous request by the client. It means that the server would like to shut down this unused connection. This response is used much more since some browsers, like Chrome, Firefox 27+, or IE9, use HTTP pre-connection mechanisms to speed up surfing. Also note that some servers merely shut down the connection without sending this message.

#### 409 Conflict
- This response is sent when a request conflicts with the current state of the server.

#### 410 Gone
- This response is sent when the requested content has been permanently deleted from server, with no forwarding address. Clients are expected to remove their caches and links to the resource. The HTTP specification intends this status code to be used for "limited-time, promotional services". APIs should not feel compelled to indicate resources that have been deleted with this status code.

#### 411 Length Required
- Server rejected the request because the Content-Length header field is not defined and the server requires it.

#### 412 Precondition Failed
- The client has indicated preconditions in its headers which the server does not meet.

#### 413 Payload Too Large
- Request entity is larger than limits defined by server. The server might close the connection or return an Retry-After header field.

#### 414 URI Too Long
- The URI requested by the client is longer than the server is willing to interpret.

#### 415 Unsupported Media Type
- The media format of the requested data is not supported by the server, so the server is rejecting the request.

#### 416 Range Not Satisfiable
- The range specified by the Range header field in the request cannot be fulfilled. It's possible that the range is outside the size of the target URI's data.

#### 417 Expectation Failed
- This response code means the expectation indicated by the Expect request header field cannot be met by the server.

#### 418 I'm a teapot
- The server refuses the attempt to brew coffee with a teapot.

#### 421 Misdirected Request
- The request was directed at a server that is not able to produce a response. This can be sent by a server that is not configured to produce responses for the combination of scheme and authority that are included in the request URI.

#### 422 Unprocessable Content (WebDAV)
- The request was well-formed but was unable to be followed due to semantic errors.

#### 423 Locked (WebDAV)
- The resource that is being accessed is locked.

#### 424 Failed Dependency (WebDAV)
- The request failed due to failure of a previous request.

#### 425 Too Early Experimental
- Indicates that the server is unwilling to risk processing a request that might be replayed.

#### 426 Upgrade Required
The server refuses to perform the request using the current protocol but might be willing to do so after the client upgrades to a different protocol. The server sends an Upgrade header in a 426 response to indicate the required protocol(s).

#### 428 Precondition Required
- The origin server requires the request to be conditional. This response is intended to prevent the 'lost update' problem, where a client GETs a resource's state, modifies it and PUTs it back to the server, when meanwhile a third party has modified the state on the server, leading to a conflict.

#### 429 Too Many Requests
- The user has sent too many requests in a given amount of time ("rate limiting").

#### 431 Request Header Fields Too Large
- The server is unwilling to process the request because its header fields are too large. The request may be resubmitted after reducing the size of the request header fields.

#### 451 Unavailable For Legal Reasons
- The user agent requested a resource that cannot legally be provided, such as a web page censored by a government.  

## Server error responses
#### 500 Internal Server Error
- The server has encountered a situation it does not know how to handle.

#### 501 Not Implemented
- The request method is not supported by the server and cannot be handled. The only methods that servers are required to support (and therefore that must not return this code) are GET and HEAD.

#### 502 Bad Gateway
- This error response means that the server, while working as a gateway to get a response needed to handle the request, got an invalid response.

#### 503 Service Unavailable
- The server is not ready to handle the request. Common causes are a server that is down for maintenance or that is overloaded. Note that together with this response, a user-friendly page explaining the problem should be sent. This response should be used for temporary conditions and the Retry-After HTTP header should, if possible, contain the estimated time before the recovery of the service. The webmaster must also take care about the caching-related headers that are sent along with this response, as these temporary condition responses should usually not be cached.

#### 504 Gateway Timeout
- This error response is given when the server is acting as a gateway and cannot get a response in time.

#### 505 HTTP Version Not Supported
- The HTTP version used in the request is not supported by the server.

#### 506 Variant Also Negotiates
- The server has an internal configuration error: the chosen variant resource is configured to engage in transparent content negotiation itself, and is therefore not a proper end point in the negotiation process.

#### 507 Insufficient Storage (WebDAV)
- The method could not be performed on the resource because the server is unable to store the representation needed to successfully complete the request.

#### 508 Loop Detected (WebDAV)
- The server detected an infinite loop while processing the request.

#### 510 Not Extended
- Further extensions to the request are required for the server to fulfill it.

#### 511 Network Authentication Required
- Indicates that the client needs to authenticate to gain network access.