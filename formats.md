# Formats

Even if the source data of video files are available as an `ArrayBuffer` are they merely usable by them-self. In general videos are packaged in different container formats which contains meta information along the actual content. Whether its video, audio or text tracks for subtitles - they all are stored inside a container to provide additional benefits. Aside of the overall compression, many formats offer an integrity check. This allows them split source files into smaller chunks and distributed them via HTTP Live Streaming (HLS) or Dynamic Adaptive Streaming Over HTTP (DASH), which is e.g. used by Youtube and Netflix.

Here is an overview about the most commonly used formats and codecs currently used at the web:

|       | MP4                   | WebM          |
| --    | --                    | --            |
| Audio | AAC                   | Vorbis, Opus  |
| Video | H.264 (MPEG-4 AVC)    | VP8/9         |

Since MP4 is available since ... and has a good support among the browsers
(including firefox regarding that the systems provides the codecs itself),
it was long time the best option. This starts to change with the spreading adoption
of WebM which was specificly designed for the web and is basically a restricted
matroskva format. // derivate
Browser support by Edge and Safari is still missing




To access the actual audio track, the container needs to be demuxed
in their original components.