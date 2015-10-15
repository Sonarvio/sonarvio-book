# Formats

Even after retrieving and assembling the source data of a video file its current content is merely usable for processing. In general videos are packaged in different container formats which contains meta information along the actual content. Whether its video, audio or text tracks for subtitles - they all are stored inside a container to provide additional benefits. Aside of the overall compression, many formats offer an redundancy check to ensure integrity. This allows them split source files into smaller chunks and distributed them via HTTP Live Streaming (HLS) or Dynamic Adaptive Streaming Over HTTP (DASH), which is e.g. used by Youtube and Netflix.

Here is an overview about the most commonly formats and codecs currently used at the web:

|       | MP4                   | WebM          |
| --    | --                    | --            |
| Audio | AAC                   | Vorbis, Opus  |
| Video | H.264 (MPEG-4 AVC)    | VP8/9         |

Since MP4 is available a bit longer and has good browser support compared to the alternatives (lately even Firefox if the systems provides the dependencies), it was a long time the best option in conjunction with OGV. This starts to change with the spreading adoption of WebM, which was specifically designed for the internet and is basically a restricted Matroska container. The [latest data](http://caniuse.com/#feat=webm) show that only Apples Safari and Microsofts Edge browser are missing support.

Whatever format got used, it first needs be decoded to access the original audio track. Originally a custom binary parser for both format was created, but canceled in favor for a more extensible solution. Instead of writing a decoder from scratch, an optimized emscripted FFmpeg port is used for the converter. In contrast to other implementations using [Emscripten](http://kripken.github.io/emscripten-site/), it provides specific builds for each container to include only a minimal subset of the regular codecs to reduce the filesize. Moreover it takes advantage of technologies like WebWorkers and asm.js for a better performance.

Integrating these builds in a browser extension lead to another challenge: Web Workers can't use the referenced Scripts. Its another CORS issue and for full disclosure it should be mentioned that Web Workers in general can't use scripts from another origin. Browser vendors often provide their own context to create an isolated environment for external extensions and plugins. Handling the conversion through a worker prevents blocking the main thread of other JavaScript executions and would be necessary for extensive computations. In the end a proxy system got created to solve this problem. It works as following:

1. an iframe is dyanmically created which points to a HTML on the other domain
2. the HTML file references a script which adds a listener for PostMessages and works as a proxy for commands send from the iframes parent window
3. the proxy script creates a new web worker with the demanded script from the same origin
4. an API for the local script is defined to exchange messages with the receiving remote script	and return values

Afterwards an ongoing issue with the [compatibility of the opus audio codec in Chrome](https://code.google.com/p/chromium/issues/detail?id=409402) was experienced, which lead to an intermediate WAV format conversion.