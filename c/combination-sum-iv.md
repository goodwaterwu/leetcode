[377. Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/description/)

```c
/* 1. Combination Sum IV */
/* Bottom-Up tabulation */
int combinationSum4(int* nums, int numsSize, int target) {
    /* Create a DP array to store the number of combinations for each value up to target */
    unsigned long long int *dp = (unsigned long long int *)calloc((target + 1), sizeof(unsigned long long int));
    /* Variable to store the final number of combinations */
    unsigned long long int combinations = 0;

    /* Base case: there is 1 way to reach target 0 (choose nothing) */
    dp[0] = 1;
    /* Iterate over all targets from 1 to target */
    for (int i = 1; i < target + 1; i++) {
        /* Try every number in nums to form current target i */
        for (int j = 0; j < numsSize; j++) {
            if (i >= nums[j])
                /* Add combinations that can reach (i - nums[j]) */
                dp[i] += dp[i - nums[j]];
        }
    }

    /* The total number of combinations to reach target */
    combinations = dp[target];
    /* Free allocated memory */
    free(dp);

    return combinations;
}
```

```c
/* 1. Combination Sum IV */
/* Top-Down memoization */

/* Helper function to calculate combinations recursively with memoization */
int helper(int* nums, int numsSize, int target, unsigned long long int *memo) {
    /* Variable to store combinations for current target */
    unsigned long long int combinations = 0;

    /* Base case: target 0 can be reached in 1 way (choose nothing) */
    if (target == 0)
        return 1;

    /* Try every number in nums to reduce current target */
    for (int i = 0; i < numsSize; i++) {
        if (target >= nums[i]) {
            /* If result already computed, use memoized value */
            if (memo[target - nums[i]] != -1)
                combinations += memo[target - nums[i]];
            else
                /* Otherwise, compute recursively */
                combinations += helper(nums, numsSize, target - nums[i], memo);
        }
    }

    /* Store the computed combinations for current target */
    memo[target] = combinations;

    return combinations;
}

/* Main function to calculate total combinations */
int combinationSum4(int* nums, int numsSize, int target) {
    /* Allocate memoization array */
    unsigned long long int *memo = (unsigned long long int *)malloc((target + 1) * sizeof(unsigned long long int));
    unsigned long long int combinations = 0;

    /* Initialize memo array with -1 indicating uncomputed values */
    for (int i = 0; i < target + 1; i++)
        memo[i] = -1;

    /* Compute total combinations using helper function */
    combinations = helper(nums, numsSize, target, memo);

    /* Free allocated memory */
    free(memo);

    return combinations;
}
```
