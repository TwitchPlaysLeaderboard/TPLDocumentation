Endpoint: ``/songs/``
-------------------------

+---------------+---------------+
| URL           | Description   |
+===============+===============+
| /songs        | The current   |
|               | song metadata |
|               | file in JSON  |
|               | format        |
|               | grouped by    |
|               | game.         |
+---------------+---------------+
| /songs/curren | The song that |
| t             | is currently  |
|               | playing on    |
|               | stream (10    |
|               | second        |
|               | delay).       |
+---------------+---------------+
| /songs/histor | Songs that    |
| y/tokens      | are           |
|               | unavailable   |
|               | as they have  |
|               | been          |
|               | requested by  |
|               | a user within |
|               | the last 6    |
|               | hours.        |
+---------------+---------------+
| /songs/histor | The most      |
| y/tokens/popu | popular       |
| lar           | requested     |
|               | songs         |
|               | including     |
|               | last bid and  |
|               | highest       |
|               | recorded bid. |
+---------------+---------------+
| /songs/histor | The last      |
| y/played      | played songs  |
|               | on stream     |
|               | (including    |
|               | non token     |
|               | songs).       |
+---------------+---------------+
| /songs/histor | Details of    |
| y/[song-id]   | the song      |
|               | specified by  |
|               | ``[song-id]`` |
|               | including     |
|               | whether the   |
|               | song is       |
|               | available for |
|               | bidding and   |
|               | the last      |
|               | bidder if not |
|               | available.    |
+---------------+---------------+