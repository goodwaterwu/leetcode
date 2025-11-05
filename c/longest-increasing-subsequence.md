[300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)

```c
/* 300. Longest Increasing Subsequence */

/* Bottom-Up tabulation */

int lengthOfLIS(int* nums, int numsSize) {
    int *dp = (int *)malloc(numsSize * sizeof(int));  /* dp[i] stores the LIS ending at index i */
    int longest = 1;  /* Tracks the overall longest increasing subsequence length */

    for (int i = 0; i < numsSize; i++)
        dp[i] = 1;  /* Each element starts as an LIS of length 1 */

    for (int i = 1; i < numsSize; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[i] > nums[j])
                if (dp[j] + 1 > dp[i])
                    dp[i] = dp[j] + 1;  /* Update dp[i] if a longer LIS ending at i is found */
        }
    }

    for (int i = 0; i < numsSize; i++)
        if (dp[i] > longest)
            longest = dp[i];  /* Track the maximum LIS length */

    free(dp);

    return longest;  /* Return the length of the longest increasing subsequence */
}
```
