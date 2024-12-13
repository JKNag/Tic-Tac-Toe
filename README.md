# Tic-Tac-Toe
package com.mycompany.tic_tac_toe;

import java.util.Scanner;

class GameInterface {
    char[][] board = new char[3][3];
    char currentPlayer = 'X';

    void initializeBoard() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                board[i][j] = ' ';
            }
        }
    }

    
    void displayBoard() {
        System.out.println("-------------");
        for (int i = 0; i < 3; i++) {
            System.out.print("| ");
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j] + " | ");
            }
            System.out.println();
            System.out.println("-------------");
        }
    }

 
    void switchPlayer() {
        if (currentPlayer == 'X') {
            currentPlayer = 'O';
        } else {
            currentPlayer = 'X';
        }
    }
}

class TicTacToe extends GameInterface {
    
    boolean makeMove(int row, int col) {
        if (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != ' ') {
            return false; 
        }
        board[row][col] = currentPlayer;
        return true;
    }


    boolean checkWin() {

        for (int i = 0; i < 3; i++) {
            if (board[i][0] == currentPlayer && board[i][1] == currentPlayer && board[i][2] == currentPlayer) {
                return true;
            }
            else if (board[0][i] == currentPlayer && board[1][i] == currentPlayer && board[2][i] == currentPlayer) {
                return true;
            }
        }
        if (board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) {
            return true;
        }
        else if (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer) {
            return true;
        }
        return false;
    }

    
    boolean isFull() {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == ' ') {
                    return false;
                }
            }
        }
        return true;
    }
}

public class Tic_Tac_Toe {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        TicTacToe game = new TicTacToe();

        while (true) {
            game.initializeBoard();
            game.currentPlayer = 'X'; 
            System.out.println("Welcome to Tic Tac Toe!");
            game.displayBoard();

            while (true) {
                System.out.println("Player " + game.currentPlayer + ", enter your move (row and column: 1 2): ");
                int row = input.nextInt() - 1;
                int col = input.nextInt() - 1;

                if (game.makeMove(row, col)) {
                    game.displayBoard();

                    if (game.checkWin()) {
                        System.out.println("Player " + game.currentPlayer + " wins!");
                        break;
                    }

                    if (game.isFull()) {
                        System.out.println("It's a draw!");
                        break;
                    }

                    game.switchPlayer();
                } else {
                    System.out.println("Invalid move, try again.");
                }
            }

            System.out.println("Do you want to play again? (yes/no): ");
            String choice = input.next().toLowerCase();

            if (!choice.equals("yes")) {
                System.out.println("Thank you for playing! Goodbye!");
                break;
            }

        }

        input.close();
    }
}
