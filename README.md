# Snake
import java.util.*;


public class Main{
    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);
        String soz = "YES";

        int record = 0;

        while(soz.equals("YES")) {
            System.out.println("Move: w,a,s,d");
            LinkedList<Integer> row = new LinkedList<>();
            LinkedList<Integer> col = new LinkedList<>();
            char[][] board = new char[12][12];

            row.add(5);
            row.add(5);
            row.add(5);
            col.add(5);
            col.add(4);
            col.add(3);


            for (int i = 0; i < 12; i++) {
                for (int j = 0; j < 12; j++) {

                    if (i == 0 || i == 11 || j == 0 || j == 11) {
                        board[i][j] = '#';
                    } else {
                        board[i][j] = '.';
                    }
                }
            }

            board[row.get(0)][col.get(0)] = 'O';
            for (int i = 1; i < row.size(); i++) {
                board[row.get(i)][col.get(i)] = 'o';
            }


            int ra = 0;
            int ca = 0;
            int rr = 0;
            int cr = 0;
            int arow = 0;
            int acol = 0;
            int d = 0;

            while (d == 0 || board[ra][ca] != '#' && board[ra][ca] != 'o') {
                if (d == 1) {


                    if (board[ra][ca] != 'a') {
                        rr = row.removeLast();
                        cr = col.removeLast();
                    }

                    row.addFirst(ra);
                    col.addFirst(ca);

                }

                if (ra != 0 || ca != 0) {
                    if (board[ra][ca] != 'a') {
                        board[rr][cr] = '.';
                    } else {
                        arow = 0;
                        acol = 0;
                    }
                    board[ra][ca] = 'O';
                    board[row.get(1)][col.get(1)] = 'o';

                }

                if (arow == 0 && acol == 0) {
                    arow = (int) (Math.random() * 10) + 1;
                    acol = (int) (Math.random() * 10) + 1;
                    while (board[arow][acol] == 'o' || board[arow][acol] == 'O') {

                        arow = (int) (Math.random() * 10) + 1;
                        acol = (int) (Math.random() * 10) + 1;

                    }
                }

                board[arow][acol] = 'a';

                for (int i = 0; i < 12; i++) {
                    for (int j = 0; j < 12; j++) {

                        System.out.print(board[i][j]);

                    }
                    System.out.println();
                }


                String move = input.next();
                d = 1;
                if (move.charAt(0) == 'w' && row.get(0) - 1 != row.get(1)) {

                    ra = row.get(0) - 1;
                    ca = col.get(0);

                } else if (move.charAt(0) == 's' && row.get(0) + 1 != row.get(1)) {

                    ra = row.get(0) + 1;
                    ca = col.get(0);

                } else if (move.charAt(0) == 'a' && col.get(0) - 1 != col.get(1)) {

                    ra = row.get(0);
                    ca = col.get(0) - 1;

                } else if (move.charAt(0) == 'd' && col.get(0) + 1 != col.get(1)) {

                    ra = row.get(0);
                    ca = col.get(0) + 1;

                } else {
                    d = 0;
                    continue;
                }


            }
            record = (int) (Math.max(row.size() - 3, record));

            System.out.println("GAME OVER");
            System.out.println("Record: " + record );
            System.out.println("Your result: " + (row.size() - 3));
            soz = "no";
            while(!soz.equals("YES")) {
                System.out.println("RESTART?");
                soz = input.next().toUpperCase();
            }

        }


    }
}
