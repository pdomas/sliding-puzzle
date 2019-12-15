import java.util.*;

public class puzzle {

    static Scanner keyboard = null;

    public static void main(String[] args) {
        System.out.println("Welcome to sliding puzzle game, the blank space is 0, here is your puzzle");

        List<Integer> initialField = new ArrayList<>();
        int numbersCounter = 0;
        for (int i = 0; i < 16; i++) {
            initialField.add(numbersCounter);
            numbersCounter++;
        }
        Collections.shuffle(initialField);
        int[][] field = new int[4][4];
        int fieldSpot = 0;
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                field[i][j] = initialField.get(fieldSpot);
                fieldSpot++;
            }
        }
       /* // For faster tesiting use this one to create field. That will allow to 'win' game faster and see if everything works as it should

        int[][] field = new int[4][4];
        field[0][0] = 1;
        field[0][1] = 2;
        field[0][2] = 3;
        field[0][3] = 4;
        field[1][0] = 5;
        field[1][1] = 6;
        field[1][2] = 7;
        field[1][3] = 8;
        field[2][0] = 9;
        field[2][1] = 10;
        field[2][2] = 11;
        field[2][3] = 12;
        field[3][0] = 13;
        field[3][1] = 14;
        field[3][2] = 0;
        field[3][3] = 15;
        */

        print(field);
        keyboard = new Scanner(System.in);
        System.out.println("Game will continue until puzzle will be resolved or you write exit");
        boolean resolved = false;
        int tileToMove;
        int selectedTileXPosition = -1, selectedTileYPosition = -1;
        int blankTileXPosition = -1, blankTileYPosition = -1;
        int movementCounter = 0;
        while (resolved == false) {
            System.out.println("Enter number which you would like to move: ");
            String input = keyboard.nextLine().trim();
            if (input.equals("exit")) {
                resolved = true;
                System.out.println("You exited the game, loser");
                System.out.println("Movements used trying to resolve this puzzle: " +movementCounter);
            }
            else {
                tileToMove = Integer.parseInt(input);
                for (int i = 0; i < 4; i++) {
                    for (int j = 0; j < 4; j++) {
                        if (field[i][j] == tileToMove) {
                            selectedTileXPosition = i;
                            selectedTileYPosition = j;
                        }
                        if (field[i][j] == 0) {
                            blankTileXPosition = i;
                            blankTileYPosition = j;
                        }
                    }
            }
                if ((Math.abs(blankTileXPosition - selectedTileXPosition) == 1 && Math.abs(blankTileYPosition - selectedTileYPosition) == 0 ) ||
                        (Math.abs(blankTileXPosition - selectedTileXPosition) == 0 && Math.abs(blankTileYPosition - selectedTileYPosition) == 1 )) {
                    field[blankTileXPosition][blankTileYPosition] = field[selectedTileXPosition][selectedTileYPosition];
                    field[selectedTileXPosition][selectedTileYPosition] = 0;
                    movementCounter++;
                }
                else {
                    System.out.println("Illegal movement, chose other number which is near 0");
                }
                    resolved = checkIfResolved(field);
                    if (resolved == true){
                        System.out.println("Congratulations, you won!");
                        System.out.println("Movements used to resolve this puzzle: " +movementCounter);
                    }
                if (resolved != true) print(field);
            }
        }

    }

    public static void print(int A[][]){
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                if (j == 0) System.out.print("|");
                if (A[i][j] < 10) System.out.print(" "+A[i][j]+"  |");
                  else System.out.print(" "+A[i][j]+" |");
            }
            System.out.println("");
        }
    }

    public static boolean checkIfResolved(int A[][]) {
        int correctStatementCounter = 1;
        int numberToCheck = 0;
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                numberToCheck++;
                if (A[i][j] == numberToCheck) correctStatementCounter++;
            }
        }
        if (correctStatementCounter == 16) return true;
        else return false;
    }

}
