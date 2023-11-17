# gameoftictactoe
#include <stdio.h>

// Function to print the Tic Tac Toe board
void printBoard(char board[3][3]) {
    printf("-------------\n");
    for (int i = 0; i < 3; i++) {
        printf("| %c | %c | %c |\n", board[i][0], board[i][1], board[i][2]);
        printf("-------------\n");
    }
}

// Function to check if a player has won
int checkWin(char board[3][3], char player) {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return 1; // Player has won
        }
    }

    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return 1; // Player has won
    }

    return 0; // No winner yet
}

// Function to check if the board is full
int isBoardFull(char board[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                return 0; // Board is not full
            }
        }
    }
    return 1; // Board is full
}

int main() {
    char board[3][3] = {{' ', ' ', ' '}, {' ', ' ', ' '}, {' ', ' ', ' '}};
    int row, col;
    char currentPlayer = 'X';

    printf("Tic Tac Toe Game\n");

    do {
        // Print the current state of the board
        printBoard(board);

        // Get the player's move
        printf("Player %c, enter your move (row and column): ", currentPlayer);
        scanf("%d %d", &row, &col);

        // Check if the chosen cell is valid
        if (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != ' ') {
            printf("Invalid move! Try again.\n");
            continue;
        }

        // Update the board with the player's move
        board[row][col] = currentPlayer;

        // Check if the current player has won
        if (checkWin(board, currentPlayer)) {
            // Print the final state of the board
            printBoard(board);
            printf("Player %c wins!\n", currentPlayer);
            break;
        }

        // Check if the board is full (a tie)
        if (isBoardFull(board)) {
            // Print the final state of the board
            printBoard(board);
            printf("It's a tie!\n");
            break;
        }

        // Switch to the other player
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';

    } while (1); // Infinite loop for the game

    return 0;
}
