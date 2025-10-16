[1. Two Sum](https://leetcode.com/problems/two-sum/description/)

```c
/* 1. Two Sum */
/*
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* twoSum(int* nums, int numsSize, int target, int* returnSize) {
    int i = 0;  /* Left index */
    int j = 1;  /* Right index (starts one ahead of i) */

    /* Allocate memory for the result array (to store 2 indices) */
    int *arr = (int *)malloc(2 * sizeof(int));

    *returnSize = 2;  /* The result will always have 2 elements (two indices) */

    /* Loop through all possible pairs of elements in nums */
    while (i < numsSize) {
        /* Check if the sum of the current pair equals the target */
        if (nums[i] + nums[j] == target) {
            arr[0] = i;  /* Store index of the first number */
            arr[1] = j;  /* Store index of the second number */
            break;        /* Exit once the correct pair is found */
        } else {
            /* If we've reached the end of the array for this i */
            if (j + 1 == numsSize) {
                i++;        /* Move i forward */
                j = i + 1;  /* Reset j to one position after i */
            } else {
                j++;        /* Otherwise, just move j forward */
            }
        }
    }

    return arr;  /* Return the indices of the two numbers that sum to target */
}
```
