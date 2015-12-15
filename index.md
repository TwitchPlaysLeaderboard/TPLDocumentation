# TwitchPlaysLeaderboard.info API Documentation

Welcome to the api documentation for TwitchPlaysLeaderboard.info. TwitchPlaysLeaderboard provides an open JSON api to developers for manipulating of the data collected from the [Twitch Plays Pokemon](http://twitch.tv/twitchplayspokemon) stream.

# Table of Contents

 [TOC]

# Getting Started

The API is publically accessible and returns data in JSON format. Requests are made using HTTP GET. The API is accessible on ```http``` or ```https``` at:  ```api.twitchplaysleaderboard.info```

All endpoints will return data in similar ways. A valid response has been returned when all the following are true:

 * The HTTP response code is 200 OK.
 * The api returned a header of ```Content-Type: application/json```
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

## API Endpoint: ```/user/```

The ```/user/``` endpoint contains user bet and balance data:

| URL | Description |
|:------------- |:-------------|
| /user/bets/[nickname] | Returns a complete collection of the users bet information for each match they bet in. |
| /user/balance/[nickname] | Return a users twitch data (nickname, color, subscriber status), last !balance and calculated balance based on bets since last !balance. |
| /user/token_matches/[nickname] | Returns a users successful bid token matches. |

## API Endpoint: ```/match/```

| URL | Description |
|:------------- |:-------------|
| /match/predict | Predicts the result of the match using [Beesafree's battle predictor](https://www.reddit.com/r/twitchplayspokemon/comments/38249f/beesafrees_battle_predictor_pbrmm/). |
| /match/current | Details of the current or last played match including pokemon and bets. |
| /match/[number] | Details of the match specified by ```[number]``` including pokemon and bets.  |
| /match/winrate | Number of played matches and number of matches won for each pokemon. |

### Endpoint: ```/match/predict/```

*Description:* Predicts the result of the match using [Beesafree's battle predictor](https://www.reddit.com/r/twitchplayspokemon/comments/38249f/beesafrees_battle_predictor_pbrmm/).

*Accepts Parameters:* 
* ```/match/predict/```: Predicts the current matchup of pokemon, returns an error if the pokemon have not yet been revealed.
* ```/match/predict/1,Ivysaur,3/4,5,6/```: Predicts the specified matchup. Request must contain exactly 6 pokemon in teams of 3. Each pokemon can either be the pokedex id or a partial name match to a pokemon. If a name matches multiple pokemon, the prediction is not ran and an error is returned stating which pokemon were matched.

#### Example: ```/match/predict/1,Ivy,3/4,5,6/```

**Description:** Example of a valid prediction request with the result data.

**Request URI:** ```https://api.twitchplaysleaderboard.info/match/predict/1,Ivy,3/4,5,6/```

```
{
	"success": true,
	"predictor": {
		"version": 4,
		"last_modified": 1446407657
	},
	"teams": {
		"blue": [
			{
				"dexNumber": 1,
				"name": "Bulbasaur",
				"visualizerIndex": "1"
			},
			{
				"dexNumber": 2,
				"name": "Ivysaur",
				"visualizerIndex": "2"
			},
			{
				"dexNumber": 3,
				"name": "Venusaur",
				"visualizerIndex": "3"
			}
		],
		"red": [
			{
				"dexNumber": 4,
				"name": "Charmander",
				"visualizerIndex": "4"
			},
			{
				"dexNumber": 5,
				"name": "Charmeleon",
				"visualizerIndex": "5"
			},
			{
				"dexNumber": 6,
				"name": "Charizard",
				"visualizerIndex": "6"
			}
		]
	},
	"speed_order": {
		"Charmander": 513.8,
		"Venusaur": 130,
		"Charmeleon": 112,
		"Charizard": 103,
		"Ivysaur": 74,
		"Bulbasaur": 71
	},
	"prediction": {
		"winner": "Red",
		"percentage": "72.60%"
	},
	"play_by_play": [
		"blue died: charmander, flareblitz has killed bulbasaur, sludgebomb in 1 turns with 100.00% hp left",
		"blue died: charmander, flareblitz has killed ivysaur, powerwhip in 1 turns with 100.00% hp left",
		"blue died: charmander, flareblitz has killed venusaur, sludge in 1 turns with  28.96% hp left"
	]
}
```

#### Example: Multiple pokemon matches ```/match/predict/1,2,3/Char,5,6/```

**Description:** Example of a prediction error that returns multiple partial name matches for `Char`.

**Request URI:** ```https://api.twitchplaysleaderboard.info/match/predict/1,2,3/Char,5,6/```

```
{
	"success": false,
	"predictor": {
		"version": null,
		"last_modified": 1446407657
	},
	"error": "Multiple results found, please be more specific",
	"error_detail": {
		"Char": [
			{
				"dexNumber": 4,
				"name": "Charmander",
				"visualizerIndex": "4"
			},
			{
				"dexNumber": 5,
				"name": "Charmeleon",
				"visualizerIndex": "5"
			},
			{
				"dexNumber": 6,
				"name": "Charizard",
				"visualizerIndex": "6"
			},
			{
				"dexNumber": 390,
				"name": "Chimchar",
				"visualizerIndex": "390"
			}
		]
	}
}
```

## API Endpoint: ```/songs/```

| URL | Description |
|:------------- |:-------------|
| /songs | The current song metadata file in JSON format grouped by game. |
| /songs/current | The song that is currently playing on stream (10 second delay). |
| /songs/history/tokens | Songs that are unavailable as they have been requested by a user within the last 6 hours. |
| /songs/history/tokens/popular | The most popular requested songs including last bid and highest recorded bid. |
| /songs/history/played | The last played songs on stream (including non token songs). |
| /songs/history/[song-id] | Details of the song specified by ```[song-id]``` including whether the song is available for bidding and the last bidder if not available. |

## API Endpoint: ```/search/```

.