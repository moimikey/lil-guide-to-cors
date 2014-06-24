Simple XHR Request
===

```
//
// XMLHttpRequest(null)                    all modern browsers and IE >= 10
// XDomainRequest(null)                    IE 8-9
// ActiveXObject('MSXML2.XMLHTTP.x.0')     IE < 7 (the value of x refers to either version 3 or 6
//
obj = XMLHttpRequest || XDomainRequest || ActiveXObject
xhr = new obj('MSXML2.XMLHTTP.6.0')
```

Pre-Flight
===

TODO

Credentialed Requests
===

A credentialed request is a request that additionally sends or sets credentials. Credentials refer to any of the following:

* HTTP Authentication ('Authorization' header)
* Client-side SSL (requests that are authenticated where the client accompanies the request with SSL certificate(s))
* Cookies ('Set-Cookie' header)

Clients that are sending a credentialed request must explicitly set the `#.withCredentials` property on the request object (in the below case, `xhr`) to `true`.

```
obj = XMLHttpRequest || XDomainRequest || ActiveXObject
xhr = new obj('MSXML2.XMLHTTP.6.0')
xhr.withCredentials = true
```

Since credentialed requests from the client trigger a pre-flight, the remote host must respond to the `OPTIONS` request with additional response headers.

Response to the `OPTIONS` request should include `Access-Control-Allow-Origin` with a value other than `*`, otherwise the pre-flight will be rejected. Values can include a single hostname, or a list of hostnames, delimited by a comma. Additionally, a `Access-Control-Allow-Credentials: true` header to ensure that the pre-flight succeeds as the server is saying that credentials being sent to it are a-ok.


FAQ
===

Q. What the hell is `X-Requested-With` and do I need it?
> `X-Requested-With` is a non-standard header that is optionally included in a request to provide identification of origin. jQuery for example sets an `X-Requested-With` header with `$.ajax` requests

Q. How would I avoid a 'pre-flight'?

> Avoid a pre-flight by:

* Not sending a credentialed request
* Not using custom headers (X-Something...), and only using the following headers:
  * Accept
  * Accept-Language
  * Content-Language
  * Last-Event-ID
  * Content-Type
* Only using GET, HEAD, POST

Q. Long-Poll vs. Short-Poll vs. Comet vs. SSE vs. WebSockets vs. PubSub
> Long-Poll: Request connection to be kept open indefinitely for x amount of time before closing and immediately reopening, repeating the pattern. Single direction.

Q. Provisional headers vs. "CAUTION: Provisional headers are shown."
> In the realm of what Chrome displays in the Network tab of your Developer Tools, while requests are pending, headers may appear incorrectly, therefore they are cautioned as provisional, as they’re subject to change.
>
> In the realm of HTTP status codes, provisional headers are non-permanent headers. They are subject to change and/or removal. The group that manages this is the IANA. All of the `Access-Control-*` headers are deemed provisional.


Citations
===

* https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
* http://www.iana.org/assignments/message-headers/message-headers.xml#perm-headers
* http://www.iana.org/assignments/message-headers/message-headers.xml#prov-headers
