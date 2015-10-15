# Solutions

The first issue to solve was the problem with Cross-Origin Resource Sharing (CORS). In general the same origin policy is a restriction by the browsers to prevent Cross Site Request Forgery (CSRF). While it normally provides security and prevents sites to send requests to other origins (protocol:domain:port), in our situation its necessary to access files which are not hosted at the same address the referrer. Since many video portals tend to use a CDN to serve their assets, supporting requests across these boundaries is mandatory. While the HTMLMediaElement like the `<video>` or `<audio>` tags are not limited by this policy - `XMLHttpRequests` done in JavaScript are.

To solve this issue, a network handler is defined which intercept all outgoing requests.At first it parses the file extension to checks if its actually one of the supported media containers. If it is, the received response headers are extended with the `Content-Allow-Origin: *` to permit access to the script. In addition the Access Control headers for `Accept-Ranges`, `Content-Encoding`, `Content-Range` and `Content-Lenght` are exposed to allow partial request for large files. This enables to create up to 6 connection to improve the average loading time.

For solving the secondary problem an anti-pattern is used by modifying native Prototypes. Normally its only done in complementary polyfill, but accessing the data stream from the outside is not possible. Therefore the initial factories are wrapped in a Closure, while keeping the same signature and exporting the same interface as the original. There is no additional attribute or side effect besides the indexing of available sources. This approach allows to keep track of its usage across the site without requiring access to the providers internals (e.g. Youtube).

```js
// SourceBuffer.prototype is not accessible - wrap factory

const BUFFERS = new WeakMap()

const addSourceBuffer = MediaSource.prototype.addSourceBuffer
MediaSource.prototype.addSourceBuffer = function (type) {
 
  const SourceBuffer = addSourceBuffer.call(this, type)
  const [ mime, codecs ] = type.split(';')

  // meta information
  BUFFERS.set(SourceBuffer, {
    'mime': mime,
    'codec': codecs.match(/codecs="(\S+)"/)[1],
    'segments': []
  })

  const appendBuffer = SourceBuffer.appendBuffer
  SourceBuffer.appendBuffer = function (data) {
    BUFFERS.get(this).segments.push(data)
    return appendBuffer.call(this, data)
  }
  return SourceBuffer
}
```

Understanding how the MediaSource Extension (MSE) API works is the key to track the required data. At first a new MediaSource is defined which is in the end set as the source of a HTMLMediaElement. Assuming a server which provides the necessary service is available, JavaScript is then used to request chunked data and append them as `SourceBuffer`.

