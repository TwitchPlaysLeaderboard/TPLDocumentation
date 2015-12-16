# TwitchPlaysLeaderboard.info API Documentation

Welcome to the api documentation for TwitchPlaysLeaderboard.info. TwitchPlaysLeaderboard provides an open JSON api to developers for manipulating of the data collected from the [Twitch Plays Pokemon](http://twitch.tv/twitchplayspokemon) stream.

# Getting Started

The API is publically accessible and returns data in JSON format. Requests are made using HTTP GET. The API is accessible on ```http``` or ```https``` at:  ```api.twitchplaysleaderboard.info```

All endpoints will return data in similar ways. A valid response has been returned when all the following are true:

 * The HTTP response code is 200 OK.
 * The api returned a header of ```Content-Type : application/json```
 * The JSON data returned a property of ```success : true```

**If the API does not return data as specified above, then an error has occurred.** 

## Callbacks

The API conforms to the JSONP specification and accepts a GET parameter ```?callback=``` which can be used to allow cross-domain API requests from your own website with JavaScript, jQuery, etc.

## Handling Errors

The API will return an error object similar to the one shown below when an error occurred. However, this is **not** the only way an error can be returned (see above).
	
```
{
"success": false,
"message": "Endpoint not found"
}
```

**Note:** In some cases, an ```exception``` will also be returned.

# API structure

The API is structured into the following categories:

| URL | Description |
|:------------- |:-------------|
| /user | User information including current balance, bet history, token match requests... |
| /match | Match results including the current match and user bet information.. |
| /songs | Song database information, token requests, current playing, recent songs... |
| /search | Searches for matches with the specified matchup or with bids from a specified user. |
