# Summary
This repository contains code for running a webserver for hosting backgammon 
tournaments between competing backgammon bots. Contestant bots also take the 
form of webservers, conforming to a simple specification.

## Contestant Spec Overview
Contestant bots are specified as the prefix that should be placed before
the following HTTP POST request endpoints:

* `/get-move`: Request provides current board state and dice-roll outcome.
Response should include the move this bot would like to make.
* `/game-started`: (Optional) Informs the bot that a new game has been started. 
If the bot returns a non-200 status code from this request, it is assumed
that the bot does not maintain internal state and doesn't bother to 
impliment this endpoint.
* `/game-over`: (Optional) Like the `/game-started`, this endpoint is not
required. The request body will include information about how the game ended, 
including whether this contestant won or lost, and whether the game was actually
completed, or one of the contestants forfeited via taking to long to respond with
their move, or responding with an illegal move.

For example, if the bot you would like to enter in the contest responds to
POST requests at `https://cleverbot.io/v42/get-move`, you would specify your bot
as simply `https://cleverbot.io/v42`.

#### `/get-move` details
Example request body:
```
{
    last_move: null,
    board: [-2, 0, 0, 0, 0, 5, 0, 2, 0, 0, 0, -5, 5, 0, 0, 0, -2, 0, -5, 0, 0, 0, 0, 2],
    bar: [0, 0],
    dice: [1, 6]
}
```