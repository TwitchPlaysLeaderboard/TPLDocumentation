
## API Endpoint: ```/songs/```

| URL | Description |
|:------------- |:-------------|
| /songs | The current song metadata file in JSON format grouped by game. |
| /songs/current | The song that is currently playing on stream (10 second delay). |
| /songs/history/tokens | Songs that are unavailable as they have been requested by a user within the last 6 hours. |
| /songs/history/tokens/popular | The most popular requested songs including last bid and highest recorded bid. |
| /songs/history/played | The last played songs on stream (including non token songs). |
| /songs/history/[song-id] | Details of the song specified by ```[song-id]``` including whether the song is available for bidding and the last bidder if not available. |
