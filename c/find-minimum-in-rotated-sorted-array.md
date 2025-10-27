[153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)

```c
/* 153. Find Minimum in Rotated Sorted Array */
/* Given a rotated sorted array nums without duplicates, find the minimum element. */

int findMin(int* nums, int numsSize) {
    int i = 0;
    int j = numsSize - 1;
    int candidate = 0; /* Index of current minimum candidate */

    while (i <= j) {
        int m = i + (j - i) / 2; /* Middle index */

        /* If current middle is smaller than current candidate, update candidate and search left half */
        if (nums[m] < nums[candidate]) {
            candidate = m;
            j = m - 1;
        } else {
            /* Otherwise search right half */
            i = m + 1;
        }
    }

    return nums[candidate]; /* Return the minimum value */
}
```
