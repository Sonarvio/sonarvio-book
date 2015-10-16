# Fingerprint

To identify an audio track, a unique signature with its characteristic features is going to be created. [Various implementations](https://musicbrainz.org/doc/Fingerprinting) of such acoustic fingerprint already exist, although only a few of them are open source and free to use. The most promising one were [Echoprint](http://echoprint.me/) and [Chromaprint](https://acoustid.org/chromaprint), but in the end neither of them actually fits for this scenario.

While most of the commercial solution use proprietary technology, Echonest was one of the first providers who shared their datasets and infrastructure. Following their acquisition by Spotify last year, their services got closed. Since then other organizations like [Mooma.sh](http://www.mooma.sh/api.html) tried to provide a matching service. None of them were capable to provide an ongoing community and shutdown after a few months.

AcoustID with Chromaprint on the contrary just had their [5th anniversay](https://oxygene.sk/2015/10/five-years-of-acoustid/) with a promising amount matching records. The problem here is the use case: Chromaprint requires full length tracks for indexing and [doesn't work with short audio snippets](https://twitter.com/lukaslalinsky/status/455067114354016257).

So far none of the open implementations that could be ported to the browser work reliable with partial content. [This severe issue](https://github.com/Sonarvio/sonarvio-editor/issues/1) has to be solved before the work at the browser extension can be continued.



