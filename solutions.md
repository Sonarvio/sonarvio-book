# Solutions

Taking on the 
Cross-Origin Resource Sharing (CORS)

In general the same origin policy is a restriction by the browsers to prevent Cross Site Request Forgery (CSRF). While it normaly provides security and prevents sites to send requests to other origins (protocol:domain:port), in our situation its neccessary to access files which are not hosted at the same address the refer. The reason is, that forinstance many video portals tend to use a Content Delivery Network (CDN) to serve their assets, as they promise faster access and constant availabilty through improved load balancing. While the HTMLMediaElement in form of '<video>' or '<audio>' tags are not limited by this policy - XMLHttpRequests done in JavaScript are.

To solve this issue, a network handler is setup which intercept all outgoing requests.

At first it parses the extension of the requested file and checks if its one of the
supported media containers. If it is, the received response headers are extended with
the 'Content-Allow-Origin: *' to permit access through the browser extension.

//

In addition the Access Control headers for 'Accept-Ranges', 'Content-Encoding',
'Content-Range' and 'Content-Lenght' are exposed to allow partial request for improved loading.
