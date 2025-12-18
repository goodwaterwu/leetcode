[338. Counting Bits](https://leetcode.com/problems/counting-bits/description/)

```c
/* 338. Counting Bits */
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* countBits(int n, int* returnSize) {
    /* Allocate memory for the dp array to store bit counts from 0 to n */
    int *dp = (int *)malloc((n + 1) * sizeof(int));

    /* Offset represents the most recent power of two */
    int offset = 1;

    /* Base case: number of 1 bits in 0 is 0 */
    dp[0] = 0;

    /* Compute the number of 1 bits for each number from 1 to n */
    for (int i = 1; i <= n; i++) {
        /* Update offset when reaching the next power of two */
        if (i == offset * 2)
            offset = i;

        /* dp[i] equals 1 plus the number of bits in i - offset */
        dp[i] = 1 + dp[i - offset];
    }

    /* Set the return size to n + 1 */
    *returnSize = n + 1;

    /* Return the result array */
    return dp;
}
```
