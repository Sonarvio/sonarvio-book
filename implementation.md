# Implementation

Through the features of the Web Audio, the original approach to retrieve the source data was straight forward and should be handled in a few lines of code.


```js
// assuming a video is available in the DOM as: <video src="..." id="video"/>
var uncompressedData = []

var atx = new AudioContext()
var source = atx.createMediaElementSource(document.getElementById('video'))

var processor = atx.createScriptProcessor()
processor.onaudioprocess = function (e) {
	var inputBuffer = e.inputBuffer
	var maxChannels = inputBuffer.numberOfChannels
	for (var channel = 0; channel < maxChannels; channel++) {
		var input = inputBuffer.getChannelData(channel)
		uncompressedData.push(input)
	}
}

source.connect(processor)
processor.connect(atx.destination)
```

In theory the `uncompressedData` could then be further used to create an acoustic fingerprint to compare the source with others. Unfortunately the Web Audio API, especially the [MediaElementAudioSource](https://developer.mozilla.org/en-US/docs/Web/API/MediaElementAudioSourceNode), has some less documented issues.

Running the code above might work in some cases, but these circumstances don't apply to the browser extension. The first error thrown during the initial test run at vimeo was the following:

``
MediaElementAudioSource outputs zeroes due to CORS access restrictions for https://fpdl.vimeocdn.com/vimeo-prod-skyfire-std-us/01/3062/5/140311923/419325727.mp4?token=5613adbf_0x15edffbe0e8a3788100c62253c94285bad8dafde
``

Since they use a Content Delivery Network (CDN) from another origin, the content will have limited access similar like a tainted Canvas. Another problem occurs on streaming data, as the source itself is not completely available and the buffer is going to be filled during the runtime. As this approach is used at Youtube and will likely be used more often in the future by different sites - its critical to tap into these streamed data as well. Doing it in an uncontrolled environment leads to another problem:

``
Uncaught InvalidStateError: Failed to execute 'createMediaElementSource' on 'AudioContext': HTMLMediaElement already connected previously to a different MediaElementSourceNode
``

The Web Audio API uses a setup of connecting nodes for in- and output. Putting this flow together enables developers to work on the underlying data with a minimal overhead, but it requires knowledge about the overall structure. Once a node is used in an active channel - its internals can't be accessed from another node.