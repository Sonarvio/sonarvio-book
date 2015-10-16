# Alternatives

As the work at the browser extension is paused, other approaches to identify a song are added to the web application. 

For once there is the option to search for tracks by using lyrics. The [musixmatch service](https://developer.musixmatch.com/) allows 2000 requests per day for non-commercial tasks and were meant to be the source provider for this matching. Since it requires some time to get an activated account, for the time a simple scraper based on [lyics.net](http://lyrics.net) is used.

Another option will be the possibility to find a song by specifying a movie or show. The client for the tunefind API is already implemented and will be used through a user interface in the next step.

Taking recordings from a file or the microphone got postponed for the same reason as the extension - an proper print algorithm is necessary to workaround the limited amount of time and background noises.