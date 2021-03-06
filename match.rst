Endpoint: ``/match/``
-------------------------

+------------------------------+------------------------------+
| URL                          | Description                  |
+==============================+==============================+
| /match/predict               | Predicts the                 |
|                              | result of the                |
|                              | match using                  |
|                              | `Beesafree’s                 |
|                              | battle                       |
|                              | predictor`_.                 |
+------------------------------+------------------------------+
| /match/current               | Details of                   |
|                              | the current                  |
|                              | or last                      |
|                              | played match                 |
|                              | including                    |
|                              | pokemon and                  |
|                              | bets.                        |
+------------------------------+------------------------------+
| /match/[number]              | Details of                   |
|                              | the match                    |
|                              | specified by                 |
|                              | ``[number]``                 |
|                              | including                    |
|                              | pokemon and                  |
|                              | bets.                        |
+------------------------------+------------------------------+
| /match/winrate               | Number of                    |
|                              | played                       |
|                              | matches and                  |
|                              | number of                    |
|                              | matches won                  |
|                              | for each                     |
|                              | pokemon.                     |
+------------------------------+------------------------------+

------------

Endpoint: ``/match/predict``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Description:* Predicts the result of a matchup using `Beesafree’s battle predictor`_.

*Accepts Parameters:*

-  ``None``: Predicts the current matchup of pokemon, returns
   an error if the pokemon have not yet been revealed.
-  ``/match/predict/1,Ivysaur,3/4,5,6/``: Predicts the specified
   matchup. Request must contain exactly 6 pokemon in teams of 3. Each
   pokemon can either be the pokedex id or a partial name match to a
   pokemon. If a name matches multiple pokemon, the prediction is not
   ran and an error is returned stating which pokemon were matched. If
   the pokemon has multiple forms you can use the form name after the pokedex
   id or in the full name **Example:** ``493water`` OR ``Arceus Water``

*Returns:*

| When a successful request is made, the API will return a JSON object structured as follows:
| See the `Example: Successful prediction request`_ below.

- ``success`` will be ``true``
- ``predictor`` contains details on the prediction engine used such as the 
  internal version number and the date the unix timestamp that the predictor was last updated.
- ``teams`` contains two properties ``blue`` and ``red`` that are arrays 
  with three keys containing the details of the pokemon for each prediction team.
  
  Each pokemon object will contain these properties:
  
  - ``dexNumber`` The pokedex id of the pokemon that was matched
  - ``name`` The full name of the pokemon including subtypes like ``Arceus Water``
  - ``visualizerIndex`` A text string that is the input needed match this pokemon when in a request 
    URL used by `TPPVisuals`_
  
- ``speed_order`` is a collection of pokemon names and their speed number, sorted fastest to slowest.
  All 6 pokemon are listed in the collection, they are NOT grouped by team.
- ``prediction`` contains the following properties:

  - ``winner`` The name of the team that is predicted to win.
  - ``percentage`` The predicted win percentage for the specified team.
  
- ``play_by_play`` is an array that lists how the battle would proceed in a perfect environment.
  Which pokemon defeats which and with how many moves.

------------
   
Example: Successful prediction request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Description:** Example of a valid prediction request with the returned result data.

**Request URI:**
``https://api.twitchplaysleaderboard.info/match/predict/1,Ivy,3/4,5,6/``

**Note:** In addition to the returned error data below, the request will also be a ``HTTP 400 Bad Request``.

::

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

Example: Failed request with multiple possible matches
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Description:** Example of a prediction error that returns multiple
partial name matches for ``Char`` and therefore the request fails.

**Request URI:**
``https://api.twitchplaysleaderboard.info/match/predict/1,2,3/Char,5,6/``

::

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

------------

Endpoint: ``/match/current``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Description:* Details of the current or last played match including pokemon and bets.

*Accepts Parameters:* ``None``

*Returns:*

------------

Endpoint: ``/match/[number]``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Description:* Details of the match specified by ``[number]`` including pokemon and bets.

*Accepts Parameters:* ``[number]`` The match number to be loaded.

*Returns:*

------------

Endpoint: ``/match/winrate``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Description:* Number of played matches and number of matches won for each pokemon.

*Accepts Parameters:* ``None`` 

*Returns:*


.. _Beesafree’s battle predictor: https://www.reddit.com/r/twitchplayspokemon/comments/38249f/beesafrees_battle_predictor_pbrmm/
.. _TPPVisuals: http://tppvisuals.com