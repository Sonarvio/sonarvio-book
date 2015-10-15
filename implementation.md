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
