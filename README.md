# Spiral-Matrix-III

You start at the cell (rStart, cStart) of an rows x cols grid facing east. The northwest corner is at the first row and column in the grid, and the southeast corner is at the last row and column.

You will walk in a clockwise spiral shape to visit every position in this grid. Whenever you move outside the grid's boundary, we continue our walk outside the grid (but may return to the grid boundary later.). Eventually, we reach all rows * cols spaces of the grid.

Return an array of coordinates representing the positions of the grid in the order you visited them.


Example 1:


Input: rows = 1, cols = 4, rStart = 0, cStart = 0
Output: [[0,0],[0,1],[0,2],[0,3]]
Example 2:


Input: rows = 5, cols = 6, rStart = 1, cStart = 4
Output: [[1,4],[1,5],[2,5],[2,4],[2,3],[1,3],[0,3],[0,4],[0,5],[3,5],[3,4],[3,3],[3,2],[2,2],[1,2],[0,2],[4,5],[4,4],[4,3],[4,2],[4,1],[3,1],[2,1],[1,1],[0,1],[4,0],[3,0],[2,0],[1,0],[0,0]]
 

Constraints:

1 <= rows, cols <= 100
0 <= rStart < rows
0 <= cStart < cols

# SOLUTION 

* Intuition
The problem requires us to traverse a grid in a spiral order starting from a given cell. The idea is to simulate the spiral traversal while keeping track of the cells we visit. Since we need to visit every cell in the grid, we can accomplish this by iterating in a controlled manner.

* Approach
Direction Array: Define the directions for moving right, down, left, and up.

* Initialize Variables:

num_steps to keep track of the steps taken in the current direction.
total_cells to know the total number of cells in the grid.
result to store the coordinates of the visited cells.
r, c for the starting coordinates, d to keep track of the current direction.

Main Loop:

Continue until we have visited all cells.
For each direction (two passes per loop to ensure the spiral expands outward).
Move in the current direction and check if the cell is within bounds.
If within bounds, add the cell to the result.
Change direction after completing the required steps.
Increase the number of steps after completing a full cycle of directions.

* Complexity
  
Time complexity: O(rows×cols)

Space complexity: O(rows×cols)

# JAVA CODE

import java.util.*;

class Solution {

    public int[][] spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
    
        int[][] directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
        
        int numSteps = 1;
        
        int totalCells = rows * cols;
        
        List<int[]> result = new ArrayList<>();
        
        int r = rStart, c = cStart;
        
        int d = 0;

        while (result.size() < totalCells) {
        
            for (int i = 0; i < 2; i++) {
            
                for (int j = 0; j < numSteps; j++) {
                
                    if (0 <= r && r < rows && 0 <= c && c < cols) {
                    
                        result.add(new int[]{r, c});
                    }
                    
                    if (result.size() == totalCells) {
                    
                        return convertListToArray(result);
                    }
                    
                    r += directions[d][0];
                    
                    c += directions[d][1];
                }
                
                d = (d + 1) % 4;
            }
            
            numSteps++;
        }

        return convertListToArray(result);
    }

    private int[][] convertListToArray(List<int[]> list) {
    
        int[][] array = new int[list.size()][2];
        
        for (int i = 0; i < list.size(); i++) {
        
            array[i] = list.get(i);
        }
        return array;
    }

    public static void main(String[] args) {
    
        Solution solution = new Solution();
        
        int[][] result = solution.spiralMatrixIII(5, 6, 1, 4);
        
        for (int[] coords : result) {
        
            System.out.println(Arrays.toString(coords));
        }
        
    }
    
}
