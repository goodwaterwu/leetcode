[Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

```c
int maxProfit(int *prices, int pricesSize)
{
    /* Kadane's Algorithm */
    int buy_in = prices[0];
    int profit = 0;

    for (int i = 1; i != pricesSize; i++) {
        if (prices[i] < buy_in) {
            buy_in = prices[i];
        } else {
            if (prices[i] - buy_in > profit)
                profit = prices[i] - buy_in;
        }
    }

    return profit;
}
```
