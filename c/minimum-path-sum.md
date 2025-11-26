[64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/description/)

```c
/* 64. Minimum Path Sum */
/* Top-Down memoization */

#define min(a, b) (((a) < (b)) ? (a) : (b))

/* recursive function to find minimum path sum to bottom-right */
int minPath(int** grid, int rows, int cols, int **memo) {
    /* current cell coordinates */
    int m = rows - 1;
    int n = cols - 1;
    int upper = 0;
    int left = 0;

    /* base case: top-left corner */
    if (m == 0 && n == 0) {
        return grid[m][n];
    } 
    /* first row: can only come from left */
    else if (m == 0) {
        if (memo[m][n - 1] != -1)
            return memo[m][n - 1] + grid[m][n];
        else
            return minPath(grid, rows, cols - 1, memo) + grid[m][n];
    } 
    /* first column: can only come from above */
    else if (n == 0) {
        if (memo[m - 1][n] != -1)
            return memo[m - 1][n] + grid[m][n];
        else
            return minPath(grid, rows - 1, cols, memo) + grid[m][n];
    } 
    /* other cells: choose minimum of top or left */
    else {
        if (memo[m][n - 1] != -1)
            upper = memo[m][n - 1];
        else
            upper = minPath(grid, rows, cols - 1, memo);

        if (memo[m - 1][n] != -1)
            left = memo[m - 1][n];
        else
            left = minPath(grid, rows - 1, cols, memo);
    }

    /* store result in memo table */
    memo[m][n] = min(upper, left) + grid[m][n];

    return memo[m][n];
}

/* main function to initialize memo table and compute result */
int minPathSum(int** grid, int gridSize, int* gridColSize) {
    /* create memo table initialized to -1 */
    int **memo = (int **)malloc(gridSize * sizeof(int *));
    int lowest = 0;

    for (int i = 0; i < gridSize; i++) {
        memo[i] = (int *)malloc((*gridColSize) * sizeof(int));
        for (int j = 0; j < *gridColSize; j++)
            memo[i][j] = -1;
    }

    /* compute minimum path sum */
    lowest = minPath(grid, gridSize, *gridColSize, memo);

    /* free allocated memory */
    for (int i = 0; i < gridSize; i++)
        free(memo[i]);

    free(memo);

    return lowest;
}
```

```c
/* 64. Minimum Path Sum */
/* Bottom-Up tabulation */

#define min(a, b) (((a) < (b)) ? (a) : (b))

int minPathSum(int** grid, int gridSize, int* gridColSize) {
    /* dp is a 2D array for storing the minimum path sum to each cell */
    int **dp = (int **)malloc(gridSize * sizeof(int *));
    /* variable to store the final result */
    int lowest = 0;

    /* allocate memory for each row in dp */
    for (int i = 0; i < gridSize; i++)
        dp[i] = (int *)malloc((*gridColSize) * sizeof(int));

    /* iterate through every cell in the grid */
    for (int i = 0; i < gridSize; i++) {
        for (int j = 0; j < *gridColSize; j++) {
            /* starting point (top-left corner) */
            if (i == 0 && j == 0)
                dp[i][j] = grid[i][j];
            /* first row: can only come from the left */
            else if (i == 0)
                dp[i][j] = dp[i][j - 1] + grid[i][j];
            /* first column: can only come from above */
            else if (j == 0)
                dp[i][j] = dp[i - 1][j] + grid[i][j];
            /* other cells: choose the smaller of top or left */
            else
                dp[i][j] = min(dp[i][j - 1], dp[i - 1][j]) + grid[i][j];
        }
    }

    /* result stored at bottom-right corner */
    lowest = dp[gridSize - 1][*gridColSize - 1];

    /* free allocated memory for dp rows */
    for (int i = 0; i < gridSize; i++)
        free(dp[i]);

    /* free the dp pointer array */
    free(dp);

    /* return the minimum path sum */
    return lowest;
}
```
