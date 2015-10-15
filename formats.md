# Formats

Source data of video files even as ArrayBuffer are merely usable themself. Videos are packaged in different container formats which contains meta
information along the actual content. Wether its video, audio or text
tracks for subtitles - they all are stored inside a container to provide
additional benefits. Aside of the overall compression, many formats
offer an integraty check and ... .

This allows split the source file into smaller chunks and distributed them
via HTTP Live Streaming (HLS) or Dynamic Adaptive Streaming Over HTTP (DASH),
as used by Youtube and Netflix.

Most commonly used formats at the web are:



|       | MP4                   | WebM          |
| --    | --                    | --            |
| Audio | AAC                   | Vorbis, Opus  |
| Video | H.264 (MPEG-4 AVC)    | VP8/9         |


This allows split the source file into smaller chunks and distributed them
via HTTP Live Streaming (HLS) or Dynamic Adaptive Streaming Over HTTP (DASH),
as used by Youtube and Netflix.


Since MP4 is available since ... and has a good support among the browsers
(including firefox regarding that the systems provides the codecs itself),
it was long time the best option. This starts to change with the spreading adoption
of WebM which was specificly designed for the web and is basically a restricted
matroskva format. // derivate
Browser support by Edge and Safari is still missing




To access the actual audio track, the container needs to be demuxed
in their original components.