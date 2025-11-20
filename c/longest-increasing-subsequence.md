[300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)

```c
/* 300. Longest Increasing Subsequence */
/* Bottom-Up tabulation */

#define max(a,b) (((a) > (b)) ? (a) : (b))

int lengthOfLIS(int* nums, int numsSize) {
    /* dp[i] stores the length of the LIS ending at index i */
    int *dp = (int *)malloc(numsSize * sizeof(int));
    int longest = 1;   /* Track the overall longest increasing subsequence */

    /* Initialize all LIS lengths to 1 */
    for (int i = 0; i < numsSize; i++)
        dp[i] = 1;

    /* Compute LIS for each index using previous values */
    for (int i = 1; i < numsSize; i++) {
        for (int j = 0; j < i; j++) {
            /* If nums[j] can be extended to nums[i], update dp[i] */
            if (nums[j] < nums[i])
                dp[i] = max(dp[i], dp[j] + 1);
        }
        /* Track the global maximum LIS */
        if (dp[i] > longest)
            longest = dp[i];
    }

    free(dp);  /* Free allocated memory */

    return longest;  /* Return the length of the longest increasing subsequence */
}
```
