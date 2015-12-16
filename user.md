
## API Endpoint: ```/user/```

The ```/user/``` endpoint contains user bet and balance data:

| URL | Description |
|:------------- |:-------------|
| /user/bets/[nickname] | Returns a complete collection of the users bet information for each match they bet in. |
| /user/balance/[nickname] | Return a users twitch data (nickname, color, subscriber status), last !balance and calculated balance based on bets since last !balance. |
| /user/token_matches/[nickname] | Returns a users successful bid token matches. |
