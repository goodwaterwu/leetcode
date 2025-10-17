[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

```c
/* 121. Best Time to Buy and Sell Stock */
/* Bottom-Up tabulation */

#define max(a, b) (((a) > (b)) ? (a) : (b))

int maxProfit(int* prices, int pricesSize) {
    /* Edge case: no prices available */
    if (pricesSize == 0)
        return 0;

    int min_price = prices[0];                  /* Minimum price seen so far */
    int max_profit = 0;                         /* Maximum profit achievable */
    int *dp = (int *)calloc(pricesSize, sizeof(int));

    dp[0] = 0;                                  /* No profit on first day */

    for (int i = 1; i < pricesSize; i++) {
        /* Update minimum price */
        if (min_price > prices[i])
            min_price = prices[i];

        /* Either keep previous max profit or sell today */
        dp[i] = max(dp[i - 1], prices[i] - min_price);
    }

    max_profit = dp[pricesSize - 1];
    free(dp);

    return max_profit;
}
```

```c
/* 121. Best Time to Buy and Sell Stock */
/* Bottom-Up constant space */

/* Calculate the maximum profit from a single buy-sell transaction */
int maxProfit(int* prices, int pricesSize) {
    int min_price = prices[0];  /* Track the minimum stock price so far */
    int max_profit = 0;         /* Track the maximum profit found */
    int i = 0;                  /* Iterator for traversing the price array */

    /* Loop through all prices */
    while (i < pricesSize) {
        /* If current profit is greater than max_profit, update it */
        if (prices[i] - min_price > max_profit) {
            max_profit = prices[i] - min_price;
        } else {
            /* If a smaller price is found, update min_price */
            if (prices[i] < min_price)
                min_price = prices[i];
        }
        i++;
    }

    return max_profit;  /* Return the maximum profit */
}
```
