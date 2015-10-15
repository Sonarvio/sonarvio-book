# Problems

Running the previous code might work in some cases, but these circumstances don't apply to the browser extension. The first error thrown during the initial test run at vimeo was the following:

``
MediaElementAudioSource outputs zeroes due to CORS access restrictions for https://fpdl.vimeocdn.com/vimeo-prod-skyfire-std-us/01/3062/5/140311923/419325727.mp4?token=5613adbf_0x15edffbe0e8a3788100c62253c94285bad8dafde
``

Since they use a Content Delivery Network (CDN) from another origin, the content will have limited access similar like a tainted Canvas. Another problem occurs on streaming data, as the source itself is not completely available and the buffer is going to be filled during the runtime. As this approach is used at Youtube and will likely be used more often in the future by different sites - its critical to tap into these streamed data as well. Doing it in an uncontrolled environment leads to another problem:

``
Uncaught InvalidStateError: Failed to execute 'createMediaElementSource' on 'AudioContext': HTMLMediaElement already connected previously to a different MediaElementSourceNode
``

The Web Audio API uses a setup of connecting nodes for in- and output. Putting this flow together enables developers to work on the underlying data with a minimal overhead, but it requires knowledge about the overall structure. Once a node is used in an active channel - its internals can't be accessed from another node.