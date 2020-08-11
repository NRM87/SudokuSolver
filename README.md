# SudokuSolver
program to automatically solve sudoku puzzles given 9x9 int array




public class Sudoku {
    private int[][] grid;
    private int[][][] marks;
    public Sudoku(){
        grid = new int[9][9];
        this.fillMarks();
    }
    public Sudoku(int[][] grid){ 
        this.grid = grid;
        this.fillMarks();
    }
    public boolean solve() {
             
        return true;
    }
    public String gridToString() {
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
    public String marksToString(){
        String ms = "";
        for (int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++) {
                if (j % 3 == 0) {
                    ms += " ";
                }
                ms += "[";
                for (int k = 0; k < 9; k++) {
                    ms += marks[i][j][k];
                }
                ms += "]";
            }
            if (i % 3 == 2) {
                ms += "\n";
            }
            ms += "\n";
        }
        return ms;
    }
    private void fillMarks() {
        marks = new int[9][9][9];
        for (int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++) {
                if (grid[i][j] != 0) {
                    marks[i][j][grid[i][j]-1] = grid[i][j];
                } else {
                    for (int k = 1; k <= 9; k++) {
                        marks[i][j][k-1] = k;
                    }
                }
            }
        }
        
    }
    public void reduceMarks() {
        for (int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++) {
                for (int k = 0; k < 9; k++) {
                    for (int m = 0; m < 9 ; m++) {
                        if (marks[i][j][k] == grid[i][m] || marks[i][j][k] == grid[m][j] || marks[i][j][k] == getBox((i-(i%3))/3,(j-(j%3))/3)[m]) {
                            if (marks[i][j][k] != grid[i][j]) {
                                marks[i][j][k] = 0;
                            }
                        }
                    }        
                }
            }
        }
    }
    public void fillGrid() {
    
    }
    public int[] getBox(int row, int col) {
        int[] box = new int[9];
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                box[i*3+j] = grid[i+row*3][j+col*3];
            }
        }
        return box;
    }
}
