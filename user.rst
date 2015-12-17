API Endpoint: ``/user/``
------------------------

The ``/user/`` endpoint contains user bet and balance data:

+---------------+---------------+
| URL           | Description   |
+===============+===============+
| /user/bets/[n | Returns a     |
| ickname]      | complete      |
|               | collection of |
|               | the users bet |
|               | information   |
|               | for each      |
|               | match they    |
|               | bet in.       |
+---------------+---------------+
| /user/balance | Return a      |
| /[nickname]   | users twitch  |
|               | data          |
|               | (nickname,    |
|               | color,        |
|               | subscriber    |
|               | status), last |
|               | !balance and  |
|               | calculated    |
|               | balance based |
|               | on bets since |
|               | last          |
|               | !balance.     |
+---------------+---------------+
| /user/token\_ | Returns a     |
| matches/[nick | users         |
| name]         | successful    |
|               | bid token     |
|               | matches.      |
+---------------+---------------+