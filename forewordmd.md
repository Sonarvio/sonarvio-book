# Foreword


Music is nowadays used in all kind of media to create emotion and emphasize on specific aspects of a story.Through the mass of these impressions we get during the day it can be difficult
to remember a certain song of such a moment. But even if are aware of it at the time,
it can be challenging to identify without a clue.

Assisted Content Recognition (ACR) or more specific computer assisted audio recognition can
help finding these catchy records by analyzing the track and compare it with existing entries
in a database. Services like [Shazam](http://shazam.com) and [Soundhound](http://soundhound.com)
offer this function foremost wrapped in mobile applications. At the time desktop clients are only
available for Mac. It's therefore currently often still necessary to use an additional device along the playing computer to get information about a song. Moreover it requires an output by speakers and can't be used with headphones.

_Sonarvio_ takes on to solve this issue by providing a web application that can be accessed directly in the browser without the overhead of a manual setup. Through its ubiquitous web based architecture it still relies on the major browser vendors, but can be adjusted to the needs of a specific platform as well. In contrast to similar projects it should provide following features:
- access at the majority of desktop operation systems by supporting the Mozilla Firefox and Google Chrome browsers
- an input option which doesn't require speakers output and can be used in public environments
- focus on open source technologies to ease the integration with other projects and promote the participation of contributors

On the following pages I like to share the experience I've made during the development,
from the initial design to the [online available application](http://sonarvio.com).