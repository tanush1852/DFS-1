# DFS-1

## Problem1 (https://leetcode.com/problems/flood-fill/)
## Time Complexity:O(m*n) Space Complexity:O(1)
## We perform dfs traversal by accessing every elements neighbouring nodes checking and changing its color.
class Solution {
    int[][]dirs;
    int m,n;
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        this.dirs=new int[][]{{-1,0},{1,0},{0,1},{0,-1}};
        this.m=image.length;
        this.n=image[0].length;

        int oldColor=image[sr][sc];
        if(oldColor==color)return image;

        helper(image,sr,sc,oldColor,color);
        return image;
    }


    private void helper(int[][] image,int sr,int sc,int oldColor,int color)
    {
      //base condition
     
      if(sr<0 || sc<0 || sr>=m || sc>=n)
      return;

     if(image[sr][sc]!=oldColor){
        return;
      }
      //logic
      if(image[sr][sc]==oldColor)
      {
        image[sr][sc]=color;
      }
      helper(image,sr+1,sc,oldColor,color);
      helper(image,sr-1,sc,oldColor,color);
      helper(image,sr,sc+1,oldColor,color);
      helper(image,sr,sc-1,oldColor,color);

     
    }
    
}

## Problem2 (https://leetcode.com/problems/01-matrix/)
## Time Complexity:O(m*n) Space Complexity:O(m*n)
## Marked all the unvisited nodes as -1 and all the 0 nodes are added to the queue.
## Queue is traversed and all the neighbouring nodes which are -1 are given the neighbouring  value+1 distance.
import java.util.*;

class Solution {
    int[][] dirs;
    int m, n;

    public int[][] updateMatrix(int[][] mat) {
        this.dirs = new int[][]{{-1, 0}, {0, 1}, {1, 0}, {0, -1}};
        this.m = mat.length;
        this.n = mat[0].length;

        // BFS initialization
        Queue<int[]> q = new LinkedList<>();
        
        // Step 1: Add all 0 cells to the queue and mark others as unvisited
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) {
                    q.add(new int[]{i, j});
                } else {
                    mat[i][j] = -1; // Mark unvisited cells as -1
                }
            }
        }

        // Step 2: Perform BFS from all the 0 cells
        while (!q.isEmpty()) {
            int[] curr = q.poll();
            for (int[] dir : dirs) {
                int r = curr[0] + dir[0];
                int c = curr[1] + dir[1];

                if (r >= 0 && c >= 0 && r < m && c < n && mat[r][c] == -1) {
                    mat[r][c] = mat[curr[0]][curr[1]] + 1;
                    q.add(new int[]{r, c});
                }
            }
        }

        return mat;
    }
}
