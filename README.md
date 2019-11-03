# sliding-puzzle

import java.util.*;

public class puzzle {

    static Scanner keyboard = null;

    public static void main(String[] args) {
     //   System.out.println("Welcome to sliding puzzle game, the blank space is 0, here is your puzzle");
      //  System.out.println("test");
        List<Integer> initial = new ArrayList<>();
  //      Random rand = new Random();
   //     int[] number = new int[16];
        int numbers = 0;
        for (int i = 0; i < 16; i++) {
            initial.add(numbers);
            numbers++;
        }
        Collections.shuffle(initial);

        int[][] field = new int[4][4];
        int numbers2 = 0;
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                field[i][j] = initial.get(numbers2);
                numbers2++;
            }
        }

        // printing
        print(field);
        keyboard = new Scanner(System.in);
        System.out.println("Game will continue until puzzle will be resolved or you write exit");
        boolean resolved = false;
        int tile;
        int temporaryx = -1, temporaryy = -1;
        int blankx = -1, blanky = -1;
        while (resolved == false) {
            System.out.println("Enter number which you would like to move: ");
            String input = keyboard.nextLine().trim();
            if (input.equals("exit")) {
                resolved = true;
                System.out.println("You exited the game, loser");
            }
            else {
                tile = Integer.parseInt(input);
                System.out.println(tile);
                for (int i = 0; i < 4; i++) {
                    for (int j = 0; j < 4; j++) {
                        if (field[i][j] == tile) {
                            temporaryx = i;
                            temporaryy = j;
                      //      System.out.println("Found number: " + temporaryx + " " + temporaryy);
                        }
                        if (field[i][j] == 0) {
                            blankx = i;
                            blanky = j;
                        //    System.out.println("Blank space kordinates: " + blankx + " " + blanky);
                        }
                    }
            }
                if ((Math.abs(blankx - temporaryx) == 1 && Math.abs(blanky-temporaryy) == 0 ) ||
                        (Math.abs(blankx - temporaryx) == 0 && Math.abs(blanky-temporaryy) == 1 )) {
                    field[blankx][blanky] = field[temporaryx][temporaryy];
                //    System.out.println("0 changed to - "+field[blankx][blanky]);
                //    System.out.println("changed to 0 "+field[temporaryx][temporaryy]);
                    field[temporaryx][temporaryy] = 0;
                }
                else {
                    System.out.println("Illegal movement, chose other number which is near 0");
                }

                if (field[0][0] == 1 && field[0][1] == 2 & field[0][2] == 3 && field[0][3] == 4
                        && field[1][0] == 5 && field[1][1] == 6 && field[1][2] == 7 && field[1][3] == 8
                        && field[2][0] == 9 && field[2][1] == 10 && field[2][2] == 11 && field[2][3] == 12
                        && field[3][0] == 13 && field[3][1] == 14 && field[3][2] == 15 && field[3][3] == 0) {
                    resolved = true;
                    System.out.println("Congratulations, you won!");
                }
                print(field);
            }
    //        print(field);
        }

    }

    public static void print(int A[][]){
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                if (j == 0) System.out.print("|");
                if (A[i][j] < 10) System.out.print(" "+A[i][j]+"  |");
                  else System.out.print(" "+A[i][j]+" |");
        //        System.out.print(i);
        //        System.out.print(j+" ");
            }
            System.out.println("");
        }
    }


}
