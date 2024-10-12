# Tic-Tac-Toe in Python

This project implements the classic Tic-Tac-Toe game using Python. The game is designed for two players, where Player 1 is represented by "X" and Player 2 by "O". The game board is implemented using a 3x3 matrix, and players take turns placing their marks until one wins or the game ends in a tie.

## Prerequisites

Before running the program, you need to have the following installed:

- *Python 3.x*: [Download Python](https://www.python.org/downloads/)
- *NumPy Library*: Install NumPy using the following command:

  bash
  pip install numpy
  

## Running the Game

1. Open a terminal or command prompt.
2. Navigate to the directory where the script is saved.
3. Run the script using Python:

   bash
   python "Tic tac toe.py"
   

## Code Breakdown

### Coding Part 1: Importing Libraries and Creating Empty Board

In this section, we import the necessary libraries and create an empty Tic-Tac-Toe board:

python
import numpy as np
import random
from time import sleep

def empty_board():
    board = np.array([
        [0,0,0],
        [0,0,0],
        [0,0,0]
    ])
    return(board)


### Coding Part 2: Checking for Empty Places on the Board and Randomly Placing Marks

This part contains functions to check for empty spaces and place a player's mark randomly on the board:

python
def empty_places(board):
    l = []
    for i in range(len(board)):
        for j in range(len(board)):
            if board[i][j] == 0:
                l.append((i,j))
    return(l)

def random_place(board, player):
    select = empty_places(board)
    current_location = random.choice(select)
    board[current_location] = player
    return(board)


### Coding Part 3: Evaluating for a Winner or a Tie

Here, we implement logic to check for a winner (by row, column, or diagonal) or if the game results in a tie:

python
def row_winner(board, player):
    for x in range(len(board)):
        win = True
        for y in range(len(board)):
            if board[x, y] != player:
                win = False
        if win == True:
            return(win)
    return(win)

def col_winner(board, player):
    for x in range(len(board)):
        win = True
        for y in range(len(board)):
            if board[y][x] != player:
                win = False
        if win == True:
            return(win)
    return(win)

def diag_winner(board, player):
    win = True
    for x in range(len(board)):
        if board[x, x] != player:
            win = False
    if win:
        return win
    win = True
    for x in range(len(board)):
        y = len(board) - 1 - x
        if board[x, y] != player:
            win = False
    return win

def evaluate_game(board):
    winner = 0
    for player in [1, 2]:
        if (row_winner(board, player) or
            col_winner(board, player) or
            diag_winner(board, player)):
            winner = player
    if np.all(board != 0) and winner == 0:
        winner = -1
    return winner


### Coding Part 4: Main Function to Run the Game

This is the main game loop where two players (Player 1 and Player 2) take turns, and the game evaluates after each turn for a winner:

python
def tic_tac_toe():
    board = empty_board()
    print(board)
    sleep(2)
    winner = 0
    counter = 1
    while winner == 0:
        for player in [1, 2]:
            brd = random_place(board, player)
            print(f"Board after {counter} move:")
            print(brd)
            sleep(2)
            counter += 1
            winner = evaluate_game(brd)
            if winner != 0:
                break
    return winner

# Driver code
winner = tic_tac_toe()
print(f"Winner is player: {winner}")


## Example Output

bash
[[0 0 0]
 [0 0 0]
 [0 0 0]]
Board after 1 move
[[0 0 0]
 [0 0 0]
 [1 0 0]]
Board after 2 move
[[0 0 0]
 [0 0 0]
 [1 0 2]]
...
Winner is player: 2


## Features

- *Turn-based gameplay*: The game alternates between two players.
- *Random placement*: Marks are placed randomly in empty spaces.
- *Win detection*: The game detects when a player wins by checking rows, columns, or diagonals.
- *Tie detection*: The game detects if the board is full and ends in a tie.

## License

This project is open-source and free to use.
