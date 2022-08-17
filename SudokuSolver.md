# SudokuSolver
program to automatically solve sudoku puzzles given 9x9 int array

    public class Sudoku {
        //Note: 0 represents an unsolved cell
        private int[][] grid;
        public Sudoku(int[][] grid){ //basic constructor using a double array as the grid
            this.grid = grid;
        }
        public Sudoku(){ //constructs an empty grid
            this(new int[9][9]);
        }
        public Sudoku(String num81) { //constructs the grid based on a string of 81 numbers
            grid = new int[9][9];
            for (int i = 0; i < 9; i++) {
                for (int j = 0; j < 9; j++) {
                    grid[i][j] = Character.getNumericValue(num81.charAt(i*9+j));
                }
            }
        }
        public boolean solve() { //uses backtracking recursion to brute-force the solution
            for (int i =0; i < 9; i++) {
                for (int j =0; j < 9; j++) {
                    if (grid[i][j] == 0) {
                        for (int k = 1; k <= 9; k++) {
                            if(!taken(i,j,k)) {
                                grid[i][j] = k;
                                if(this.solve()){
                                    return true;
                                } else {
                                    grid[i][j] = 0;
                                }
                            }
                        }
                        return false;
                    }
                }
            }
            return true;
        }
        public int[][] getBox(int row, int col) { //returns a 3 by 3 array representing a box of the sudoku puzzle based on the row and column, e.g. getBox(2,0) would return the bottom left box
            int[][] box = new int[3][3];
            for (int i = 0; i < 3; i++) {
                for (int j = 0; j < 3; j++) {
                    box[i][j] = grid[i+row*3][j+col*3];
                }
            }
            return box;
        }
        public boolean taken(int row, int col, int num) {//checks if a number already appears in the row, column, or box of a single cell
            for (int m = 0; m < 9 ; m++) {
                if (num == grid[row][m] || num == grid[m][col] || num == getBox((row-(row%3))/3,(col-(col%3))/3)[m/3][m%3]) {
                    return true;
                } 
            }
            return false;
        }
        public String gridToString() { //returns string representation of the sudoku grid
            String gs = "";
            for (int i = 0; i < 9; i++){
                for(int j = 0; j < 9; j++) {
                    if (j % 3 == 0) {
                        gs += " ";
                    }
                    gs += grid[i][j];
                }
                if (i % 3 == 2) {
                    gs += "\n";
                }
                gs += "\n";
            }
            return gs;
        }
    }
