# Solutions

The first issue to solve was the problem with Cross-Origin Resource Sharing (CORS). In general the same origin policy is a restriction by the browsers to prevent Cross Site Request Forgery (CSRF). While it normally provides security and prevents sites to send requests to other origins (protocol:domain:port), in our situation its necessary to access files which are not hosted at the same address the referrer. Since many video portals tend to use a CDN to serve their assets, supporting requests across these boundaries are mandatory. While the HTMLMediaElement like the '<video>' or '<audio>' tags are not limited by this policy - XMLHttpRequests done in JavaScript are.

To solve this issue, a network handler is setup which intercept all outgoing requests.

At first it parses the extension of the requested file and checks if its one of the
supported media containers. If it is, the received response headers are extended with
the 'Content-Allow-Origin: *' to permit access through the browser extension.

//

In addition the Access Control headers for 'Accept-Ranges', 'Content-Encoding',
'Content-Range' and 'Content-Lenght' are exposed to allow partial request for improved loading.
