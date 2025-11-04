[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/description/)

```c
/* 53. Maximum Subarray */

/* Bottom-Up constant space */

int maxSubArray(int* nums, int numsSize) {
    int max_sum = INT_MIN;  /* Tracks the maximum subarray sum found so far */
    int curr_sum = 0;       /* Tracks the current subarray sum */
    int i = 0;

    while (i < numsSize) {
        curr_sum += nums[i];               /* Add current element to running sum */
        if (curr_sum > max_sum)
            max_sum = curr_sum;            /* Update max_sum if current sum is larger */
        if (curr_sum < 0)
            curr_sum = 0;                  /* Reset sum if it becomes negative */
        i++;
    }

    return max_sum;  /* Return the largest subarray sum */
}
```

```c
/* 53. Maximum Subarray */

/* Bottom-Up tabulation */

#define max(a, b) (((a) > (b)) ? (a) : (b))

int maxSubArray(int* nums, int numsSize) {
    int *dp = (int *)malloc(numsSize * sizeof(int));  /* dp[i] stores the max subarray sum ending at index i */
    int max_sum = nums[0];                             /* Tracks the maximum subarray sum found so far */

    dp[0] = nums[0];  /* Initialize first element */

    for (int i = 1; i != numsSize; i++) {
        dp[i] = max(dp[i - 1] + nums[i], nums[i]);  /* Either extend previous subarray or start new at i */
        if (dp[i] > max_sum)
            max_sum = dp[i];                        /* Update maximum sum */
    }

    free(dp);

    return max_sum;  /* Return the maximum subarray sum */
}
```
