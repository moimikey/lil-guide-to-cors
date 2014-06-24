Simple XHR Request
===

```
//
// XMLHttpRequest(null)
// XDomainRequest(null)
// ActiiveXObject('MSXML2.XMLHTTP.x.0')     x = 3 || 6
//
obj = XMLHttpRequest || XDomainRequest || ActiveXObject
xhr = new obj('MSXML2.XMLHTTP.6.0')
```

Credentialed Requests
===

A credentialed request is a request that additionally sends or sets credentials. Credentials refer to any of the following:

* HTTP Authentication ('Authorization' header)
* Client-side SSL (requests that are authenticated where the client accompanies the request with SSL certificate(s))
* Cookies ('Set-Cookie' header)

Credentialed requests will be rejected during pre-flight if `Access-Control-Allow-Origin` has a value of `*` (a wildcard value). The origin must be explicitly set with a hostname or comma delimited hostnames.


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
