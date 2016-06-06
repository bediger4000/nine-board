# Nine-board Tic Tac Toe in your browser

A JavaScript implementation of 9-board Tic Tac Toe

You can [play it](https://rawgit.com/bediger4000/nine-board/master/9board.html) right now!

## Rules

A 9-board tic tac toe board consists of nine ordinary tic tac toe
boards, arranged in a 3 x 3 square. That's 81 total spots for players
to make marks. Two players compete.

The first player makes a mark in any of the 81 spots on a board. Every
move after that is constrained to the board in the 3 x 3 grid of boards
that's in the same position as the the last mark was in a small board.

Players alternate making marks.

The first play to get 3 marks in a row, horizontally, verically or
diagonally in any of the 9 ordinary tic tac toe boards wins.

### Example

![example move](https://raw.githubusercontent.com/bediger4000/nine-board/master/example.png)

In the above image, the `O` player made a move in the upper
right board, specifically in the middle left slot.

The `X` player is constrained to make their mark in any open
slot of the middle left board.  The `O` player' will be
constrained to make their second mark in the board corresponding
to the slot in which the `X` player makes a mark.

## Installation


## Design

### Static Evaluation Function
