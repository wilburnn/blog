---
title: Browser Questions
date: "2021-08-25"
description: "Browser Questions"
---

## Table of Contents

- [Origin](#origin)
- [CORS](#cors)
- [HTTP Caching](#http-caching)
- [HTMLCollection and NodeList](#htmlcollection-and-nodelist)

---

### Origin

- Web content's origin is defined by the scheme (protocol), hostname (domain), and port of the URL used to access it.
- Two objects have the same origin only when the scheme, hostname and port all match.

###### References

- [https://developer.mozilla.org/en-US/docs/Glossary/Origin](https://developer.mozilla.org/en-US/docs/Glossary/Origin)

⬆️ [Back to top](#table-of-contents)

---

### CORS

- Cross-Origin Resource Sharing (CROS) is an HTTP-header based mechanism that allows a server to indicate any origins other than its own from which a browser should permit loading of resources.
- Three scenarios:
    - Simple requests don't trigger a CORS preflight.
    - Preflighted requests.
    - Requests with credentials.

###### References

- [https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#what_requests_use_cors](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#what_requests_use_cors)

⬆️ [Back to top](#table-of-contents)

---

### HTTP Caching

- Different kinds of caches
    - Private browser caches
    - Shared proxy caches
    - Other caches......
- Terminology
    - Stale Content
    - Fresh Content
    - Cache Validation
    - Cache Invalidation
- How does the content get cached?
    - Whenever the server sends the response to the client, it sends the HTTP headers in the response, which are then used by the client or any other intermediate places to cache the content.
    - Caching headers
        - Expires
        - Pragma
        - Cache-Control
- How is the validation of cache checked from the server?
    - ETag (Entity Tags)
    - Last-Modified

⬆️ [Back to top](#table-of-contents)

---

### HTMLCollection and NodeList

HTMLCollection 

- A generic collection (array-like object similar to `arguments`) of elements (in document order) and offer methods and properties from selecting from the list.
- An `HTMLCollection` in the HTML DOM is **live**; it is automatically updated when the underlying document is changed.

NodeList
- `NodeList` objects are collections of nodes, not an `Array`.
- 2 varieties: live and static.

###### References

- [https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection)
- [https://developer.mozilla.org/en-US/docs/Web/API/NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList)

⬆️ [Back to top](#table-of-contents)
