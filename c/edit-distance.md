[72. Edit Distance](https://leetcode.com/problems/edit-distance/description/)

```c
#define min(a, b) (((a) < (b)) ? (a) : (b))

int minDistance(char* word1, char* word2) {
    int **dp = (int **)malloc((strlen(word1) + 1) * sizeof(int *));
    int min = 0;
    int i = 0;
    int j = 0;

    for (int i = 0; i < strlen(word1) + 1; i++)
        dp[i] = (int *)calloc((strlen(word2) + 1), sizeof(int));

    dp[0][0] = 0;
    for (int i = 1; i < strlen(word1) + 1; i++)
        dp[i][0] = i;
    for (int j = 1; j < strlen(word2) + 1; j++)
        dp[0][j] = j;

    if (word1[0] == '\0' || word2[0] == '\0') {
        min = dp[strlen(word1)][strlen(word2)];
        goto free_dp;
    }

    for (i = 1; i < strlen(word1) + 1; i++) {
        for (j = 1; j < strlen(word2) + 1; j++) {
            if (word1[i - 1] == word2[j - 1])
                dp[i][j] = dp[i - 1][j - 1];
            else
                dp[i][j] = min(min(dp[i - 1][j] + 1, dp[i][j - 1] + 1), dp[i - 1][j - 1] + 1);
        }
    }

    min = dp[i - 1][j - 1];
free_dp:
    for (int i = 0; i < strlen(word1) + 1; i++)
        free(dp[i]);

    free(dp);

    return min;
}
```
