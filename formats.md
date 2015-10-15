# Formats

Even after retrieving and assembling the source data of a video file its current content is merely usable for processing. In general videos are packaged in different container formats which contains meta information along the actual content. Whether its video, audio or text tracks for subtitles - they all are stored inside a container to provide additional benefits. Aside of the overall compression, many formats offer an redundancy check to ensure integrity. This allows them split source files into smaller chunks and distributed them via HTTP Live Streaming (HLS) or Dynamic Adaptive Streaming Over HTTP (DASH), which is e.g. used by Youtube and Netflix.

Here is an overview about the most commonly formats and codecs currently used at the web:

|       | MP4                   | WebM          |
| --    | --                    | --            |
| Audio | AAC                   | Vorbis, Opus  |
| Video | H.264 (MPEG-4 AVC)    | VP8/9         |

Since MP4 is available a bit longer and has good browser support compared to the alternatives (lately even Firefox if the systems provides the dependencies), it was a long time the best option in conjunction with OGV. This starts to change with the spreading adoption of WebM, which was specifically designed for the internet and is basically a restricted Matroska container. The [latest data](http://caniuse.com/#feat=webm) show that only Apples Safari and Microsofts Edge browser are missing support.

Whatever format s used - to access the actual audio track, the container needs to be demuxed
in their original components.
#

even as an ArrayBuffer