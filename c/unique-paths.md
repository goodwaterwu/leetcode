[62. Unique Paths](https://leetcode.com/problems/unique-paths/description/)

```c
/* 62. Unique Paths */
/* Top-Down memoization */

int paths(int m, int n, int **memo) {
    /* Convert to zero-based index */
    int x = m - 1;
    int y = n - 1;
    int left = 0;
    int upper = 0;
    int routes = 0;

    /* If out of bounds, no valid path */
    if (x < 0 || y < 0)
        return 0;

    /* Base case: first row or first column only has 1 path */
    if (x == 0 || y == 0) {
        memo[x][y] = 1;
        return memo[x][y];
    }

    /* If already computed, return cached value */
    if (memo[x][y] > 0)
        return memo[x][y];

    /* Calculate paths from the top cell */
    if (memo[x - 1][y] > 0)
        left = memo[x - 1][y];
    else
        left = paths(m - 1, n, memo);

    /* Calculate paths from the left cell */
    if (memo[x][y - 1] > 0)
        upper = memo[x][y - 1];
    else
        upper = paths(m, n - 1, memo);

    /* Store result in memo table */
    memo[x][y] = left + upper;

    return memo[x][y];
}

int uniquePaths(int m, int n) {
    /* Memoization table for storing intermediate results */
    int **memo = (int **)malloc(m * sizeof(int *));
    int routes = 0;

    /* Allocate and initialize memo table with zeros */
    for (int i = 0; i < m; i++)
        memo[i] = (int *)calloc(n, sizeof(int));

    /* Start recursive computation */
    routes = paths(m, n, memo);

    /* Free allocated memory */
    for (int i = 0; i < m; i++)
        free(memo[i]);

    free(memo);

    /* Return total number of unique paths */
    return routes;
}
```

```c
/* 62. Unique Paths */
/* Bottom-Up tabulation */

int uniquePaths(int m, int n) {
    /* dp[i][j] stores the number of unique paths to reach cell (i, j) */
    int **dp = (int **)malloc(m * sizeof(int *));
    int routes = 0;   /* Store final number of routes */

    /* Allocate each row of the DP table */
    for (int i = 0; i < m; i++)
        dp[i] = (int *)malloc(n * sizeof(int));

    /* Initialize first column: only 1 way (move down only) */
    for (int i = 0; i < m; i++)
        dp[i][0] = 1;

    /* Initialize first row: only 1 way (move right only) */
    for (int j = 0; j < n; j++)
        dp[0][j] = 1;

    /* Fill DP table: current cell = top cell + left cell */
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++)
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
    }

    /* The answer is stored in bottom-right corner */
    routes = dp[m - 1][n - 1];

    /* Free allocated memory */
    for (int i = 0; i < m; i++)
        free(dp[i]);

    free(dp);

    /* Return the total number of unique paths */
    return routes;
}
```
