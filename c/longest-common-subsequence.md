[1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/description/)

```c
/* 1143. Longest Common Subsequence */
/* Top-Down memoization */

#define max(a, b) (((a) > (b)) ? (a) : (b))

static int **memo;

/* Recursive helper function to compute LCS length using memoization */
int longest(char* text1, int pos1, char* text2, int pos2) {
    /* Base case: if either string index goes below 0, no subsequence remains */
    if (pos1 < 0 || pos2 < 0)
        return 0;

    /* Return memoized result if already computed */
    if (memo[pos1][pos2] != -1)
        return memo[pos1][pos2];

    /* If current characters match, move diagonally and add 1 */
    if (text1[pos1] == text2[pos2])
        memo[pos1][pos2] = longest(text1, pos1 - 1, text2, pos2 - 1) + 1;
    else
        /* Otherwise, take the maximum of moving left or up in the DP matrix */
        memo[pos1][pos2] = max(longest(text1, pos1 - 1, text2, pos2),
                               longest(text1, pos1, text2, pos2 - 1));

    return memo[pos1][pos2];
}

int longestCommonSubsequence(char* text1, char* text2) {
    int ret = 0;

    /* Allocate memory for the memoization table */
    memo = (int **)malloc(strlen(text1) * sizeof(int *));
    for (int i = 0; i < strlen(text1); i++)
        memo[i] = (int *)malloc(strlen(text2) * sizeof(int));

    /* Initialize all entries to -1 (uncomputed) */
    for (int i = 0; i < strlen(text1); i++) {
        for (int j = 0; j < strlen(text2); j++)
            memo[i][j] = -1;
    }

    /* Start recursion from the last indices of both strings */
    ret = longest(text1, strlen(text1) - 1, text2, strlen(text2) - 1);

    /* Free allocated memory after computation */
    for (int i = 0; i < strlen(text1); i++)
        free(memo[i]);
    free(memo);

    /* Return the final LCS length */
    return ret;
}
```

```c
/* 1143. Longest Common Subsequence */
/* Bottom-Up tabulation */

#define max(a, b) (((a) > (b)) ? (a) : (b))

int longestCommonSubsequence(char* text1, char* text2) {
    /* Create a 2D DP table where dp[i][j] stores the length of 
       the longest common subsequence between text1[0..i-1] and text2[0..j-1] */
    int dp[strlen(text1) + 1][strlen(text2) + 1];

    /* Initialize the DP table with zeros */
    memset(dp, 0, sizeof(dp));

    /* Build the table in a bottom-up manner */
    for (int i = 1; i < strlen(text1) + 1; i++) {
        for (int j = 1; j < strlen(text2) + 1; j++) {
            /* If the current characters match, take the diagonal value + 1 */
            if (text1[i - 1] == text2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                /* Otherwise, take the maximum of top or left cell */
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }

    /* The bottom-right cell contains the final LCS length */
    return dp[strlen(text1)][strlen(text2)];
}
```
