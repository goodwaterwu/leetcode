[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/description/)

```c
/* 53. Maximum Subarray */
/* Kadane’s Algorithm */
int maxSubArray(int* nums, int numsSize) {
    /* Initialize the maximum sum as the first element */
    int max = nums[0];
    /* Initialize the current running total as the first element */
    int total = nums[0];
    int i = 1;

    /* If there is only one element, return it directly */
    if (numsSize == 1)
        return max;

    /* Loop through the array starting from the second element */
    while (i < numsSize) {
        /* If adding the current number increases the total, keep adding */
        /* Otherwise, start a new subarray from the current number */
        if (total + nums[i] > nums[i])
            total = total + nums[i];
        else
            total = nums[i];

        /* Update the maximum sum found so far */
        if (total > max)
            max = total;

        i++;
    }

    /* Return the maximum subarray sum */
    return max;
}
```
