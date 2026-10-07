import java.util.Random;
import java.util.Scanner;

public class Game {
    public static void main(String[] args) {
        char[] board = {'1', '2', '3', '4', '5', '6', '7', '8', '9'};
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();

        char playerSymbol = 'X';
        char compSymbol = 'O';

        boolean playerTurn = random.nextBoolean();
        if (playerTurn) {
            System.out.println("Coin toss result: Player goes first!");
        } else {
            System.out.println("Coin toss result: Computer goes first!");
        }

        printBoard(board);

        while (true) {
            if (playerTurn) {
                System.out.print("Player's turn. Select a square: ");
                int playerMove = scanner.nextInt();

                board[playerMove - 1] = playerSymbol;

                printBoard(board);

                if (checkWin(board, playerSymbol)) {
                    System.out.println("Player wins!");
                    break;
                }
            } else {
                System.out.println("Computer's turn...");
                int compMove = random.nextInt(9) + 1;

                board[compMove - 1] = compSymbol;
                System.out.println("Computer placed on square " + compMove);

                printBoard(board);

                if (checkWin(board, compSymbol)) {
                    System.out.println("Computer wins!");
                    break;
                }
            }

            if (isDraw(board)) {
                System.out.println("It's a draw!");
                break;
            }

            playerTurn = !playerTurn;
        }

        scanner.close();
    }

    private static boolean checkWin(char[] b, char symbol) {
        int[][] winConditions = {
            {0, 1, 2}, {3, 4, 5}, {6, 7, 8}, // Rows
            {0, 3, 6}, {1, 4, 7}, {2, 5, 8}, // Columns
            {0, 4, 8}, {2, 4, 6}             // Diagonals
        };

        for (int[] condition : winConditions) {
            if (b[condition[0]] == symbol && b[condition[1]] == symbol && b[condition[2]] == symbol) {
                return true;
            }
        }
        return false;
    }

    private static boolean isDraw(char[] b) {
        for (char c : b) {
            if (c != 'X' && c != 'O') {
                return false;
            }
        }
        return true;
    }

    private static void printBoard(char[] b) {
        System.out.println();
        System.out.println(" " + b[0] + " | " + b[1] + " | " + b[2] + " ");
        System.out.println("---+---+---");
        System.out.println(" " + b[3] + " | " + b[4] + " | " + b[5] + " ");
        System.out.println("---+---+---");
        System.out.println(" " + b[6] + " | " + b[7] + " | " + b[8] + " ");
        System.out.println();
    }
}
