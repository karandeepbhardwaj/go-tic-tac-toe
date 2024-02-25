Creating a simple Tic Tac Toe game is a great way to get familiar with the basics of programming in Go. This beginner tutorial will guide you through the steps to build a console-based Tic Tac Toe game. We'll start with the basics of Go syntax and gradually build up our game.

### Prerequisites

- Basic understanding of programming concepts
- Go installed on your machine ([Download Go](https://golang.org/dl/))

### Step 1: Setup Your Environment

Before you start coding, make sure Go is correctly installed on your system. Open your terminal or command prompt and type:

```sh
go version
```

This command should return the version of Go installed on your system.

### Step 2: Initialize Your Go Module

Create a new directory for your project, navigate into it, and then initialize a new Go module:

```sh
mkdir tic-tac-toe
cd tic-tac-toe
go mod init tic-tac-toe
```

### Step 3: Create Your Main File

Create a file named `main.go` in your project directory. This file will contain the entry point to your game.

```sh
touch main.go
```

Open `main.go` in your favorite text editor, and let's start coding.

### Step 4: Write The Game Code

#### Step 4.1: Define the Game Board

First, we'll define the game board. Add the following code to `main.go`:

```go
package main

import "fmt"

func main() {
    // Initialize the game board with empty spaces
    board := [3][3]string{
        {" ", " ", " "},
        {" ", " ", " "},
        {" ", " ", " "},
    }

    printBoard(board)
}

// printBoard prints the current state of the board
func printBoard(board [3][3]string) {
    for i := 0; i < 3; i++ {
        for j := 0; j < 3; j++ {
            fmt.Print(board[i][j])
            if j < 2 {
                fmt.Print("|")
            }
        }
        if i < 2 {
            fmt.Println("\n-+-+-")
        }
    }
    fmt.Println()
}
```

This code initializes your Tic Tac Toe board as a 3x3 array filled with spaces, indicating empty positions. The `printBoard` function prints the board to the console.

#### Step 4.2: Add Players' Moves

Next, we'll add a function to allow players to make moves:

```go
import (
    "bufio"
    "fmt"
    "os"
    "strconv"
    "strings"
)

func makeMove(player string, board *[3][3]string) {
    var x, y int
    scanner := bufio.NewScanner(os.Stdin)

    for {
        fmt.Printf("Player %s, enter your move (row col): ", player)
        scanner.Scan()
        input := strings.Split(scanner.Text(), " ")
        if len(input) != 2 {
            fmt.Println("Invalid input. Please enter row and column as two numbers separated by a space.")
            continue
        }

        var err error
        x, err = strconv.Atoi(input[0])
        y, err = strconv.Atoi(input[1])
        if err != nil || x < 1 || x > 3 || y < 1 || y > 3 || board[x-1][y-1] != " " {
            fmt.Println("Invalid move. Try again.")
            continue
        }

        break
    }

    board[x-1][y-1] = player
}
```

This function prompts the current player to enter their move, validates the input, and updates the board accordingly.

#### Step 4.3: Implement the Game Loop

Now, let's implement the main game loop and alternate turns between two players until one wins or the game ends in a draw:

```go
func main() {
    board := [3][3]string{
        {" ", " ", " "},
        {" ", " ", " "},
        {" ", " ", " "},
    }

    currentPlayer := "X"
    for {
        printBoard(board)
        makeMove(currentPlayer, &board)
        // Switch player
        if currentPlayer == "X" {
            currentPlayer = "O"
        } else {
            currentPlayer = "X"
        }
        // Add check for win or draw here (explained in the next step)
    }
}
```

#### Step 4.4: Determine the Game Outcome

To keep this tutorial concise, I'll briefly outline how you could implement win and draw detection:

- After each move, check if the current player has won by having three of their marks in a row, column, or diagonal.
- Check if the board is full (indicating a draw) if no player has won yet.
- You can implement these checks in a function called `checkWin(board [3][3]string) bool` and `checkDraw(board [3][3]string) bool`.

### Step 5: Running Your Game

To run your game, navigate to your project directory in the terminal and execute:

```sh
go run main.go
```

### Conclusion

Congratulations! You've just created a simple Tic Tac Toe game in Go. This tutorial covered initializing a Go module, creating a game board, accepting player inputs, and implementing a game loop. To enhance your game, consider adding win and draw detection, refactoring the code to improve its organization and readability, and implementing a better AI for single-player mode.

Enjoy coding with Go!
