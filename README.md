# Nine-board Tic Tac Toe in your browser

A JavaScript implementation of 9-board Tic Tac Toe

You can [play it](https://rawgit.com/bediger4000/nine-board/master/9board.html) right now!

This is not [Ultimate Tic Tac Toe](https://mathwithbaddrawings.com/2013/06/16/ultimate-tic-tac-toe/).
The winning condition is different. Any three-in-a-row wins this game. Ultimate Tic Tac Toe
requires winning 3 subboards in a row.

## Rules

A 9-board tic tac toe board consists of nine ordinary tic tac toe
boards, arranged in a 3 x 3 square. That's 81 total spots for players
to make marks. Two players compete.

The first player makes a mark in any of the 81 spots on a board. Every
move after that is constrained to the board in the 3 x 3 grid of boards
that's in the same position as the the last mark was in a small board.

Players alternate making marks.

The first play to get 3 marks in a row, horizontally, vertically or
diagonally in any of the 9 ordinary tic tac toe boards wins.

The program enforces the rules. The first player can mark any of
the 81 slots. After that, the program won't allow itself or the human
to place a mark outside of the board corresponding to the slot of the
previous move.

### Example

![example move](https://raw.githubusercontent.com/bediger4000/nine-board/master/example.png)

In the above image, the `O` player made a move in the upper
right board, specifically in the middle left slot.

The `X` player is constrained to make their mark in any open
slot of the middle left board.  The `O` player will be
constrained to make their second mark in the board corresponding
to the slot in which the `X` player makes a mark.

## Installation

The game consists of a single HTML file. You can put it anywhere a web server can
find it, and call it with a URL.

Or, you can leave the HTML file local. Most (all?) browsers will allow you to use 
a URL with a "file" schema: `file:///home/bediger/src/javascript/nine-board/9board.html`
for example.

I would recommend a strength of 2 at the beginning. You can probably ramp up to strength
of 6, but it will win most of the time at that amount of lookahead. A strength of 8 will
probably beat every human.

## Design

This program does standard alpha-beta minimaxing. The computer assumes it's the value
maximiser, and that the human is the value minimizer. At the top level, it does keep
all of its moves that have the same value, and randomly picks from its actual move
from those candidates. This means that games are non-deterministic, even if the first
move is the same.

`function x_your_move()` is the entry into the computer's move decision code.

The user interface is mostly static HTML, but `function drawBoard()` generates
the starting board, which has 81 HTML buttons on it. Each of the 81 buttons calls
`function humanClick()` on a mouse click.

The few other buttons ("Computer goes first", "Reset", "New game") each have
"onclick" functions that enter the JavaScript and do appropriate things.
When the computer goes first, it just randomly picks one of the 81 possible
moves. Some first moves are stronger than others, I just haven't looked at
first moves deeply and systematically enough to have "book openings" for the
computer.

### Static Evaluation Function

Static evaluation is the only interesting part of the coding.  I tried to do
incremental utility, by assigning a numerical value to the move being
evaluated. `function utility()` does this assignment.  The idea was to spend
less time calculating redundant utility values at the maximum depth or at
leaves of the game tree. Unfortunately, the only
static values that get considered are for moves made during reaching the
maximum depth or the leaf nodes. I didn't include the value of the board at
the start of the computer deciding on its move. This leads to a seemlingly
more interesting computer opponent so I left this flaw un-fixed.

The value of a winnning move is given by a very large number minus the depth
of lookahead,
with an increment of 3000 for getting two-in-a-row (the next move
can win), and an increment of 1000 for blocking a win.

If no winning moves can be made, I gave it a slight bias for center-of-subboard
slots, and an even lesser bias for corner-of-subboard slots.

This JavaScript program had a PHP precursor. I determined the utility values
empirically, by playing two slightly different PHP programs against each
other.

