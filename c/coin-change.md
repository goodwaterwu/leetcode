[322. Coin Change](https://leetcode.com/problems/coin-change/description/)

```c
/* 322. Coin Change */

/* Bottom-Up tabulation */

#define min(a, b) (((a) < (b)) ? (a) : (b))

int coinChange(int* coins, int coinsSize, int amount) {
    int *dp = (int *)malloc((amount + 1) * sizeof(int));  /* dp[i] stores the fewest coins to make amount i */
    int fewest = 0;

    for (int i = 0; i != amount + 1; i++)
        dp[i] = INT_MAX;  /* Initialize all values as infinity (unreachable) */

    dp[0] = 0;  /* Base case: 0 coins needed to make amount 0 */

    for (int i = 1; i != amount + 1; i++) {
        for (int j = 0; j != coinsSize; j++) {
            if (i - coins[j] >= 0 && dp[i - coins[j]] != INT_MAX)
                dp[i] = min(dp[i], dp[i - coins[j]] + 1);  /* Choose minimum coins for current amount */
        }
    }

    if (dp[amount] == INT_MAX)
        fewest = -1;  /* If amount cannot be formed, return -1 */
    else
        fewest = dp[amount];  /* Otherwise, return the minimum coin count */

    free(dp);

    return fewest;  /* Return the fewest number of coins required */
}
```
