[518. Coin Change II](https://leetcode.com/problems/coin-change-ii/description/)

```c
/* 518. Coin Change II */

/* Bottom-Up tabulation */

int change(int amount, int* coins, int coinsSize) {
    unsigned long long int *dp = (unsigned long long int *)calloc(amount + 1, sizeof(unsigned long long int));
    unsigned long long int combinations = 0;

    dp[0] = 1;  /* Base case: one way to make amount 0 (choose no coins) */

    for (int i = 0; i < coinsSize; i++) {
        for (int j = coins[i]; j <= amount; j++) {
            dp[j] += dp[j - coins[i]];  /* Add combinations including current coin */
        }
    }

    combinations = dp[amount];  /* Total combinations to form the target amount */
    free(dp);

    return combinations;  /* Return the number of possible combinations */
}
```
