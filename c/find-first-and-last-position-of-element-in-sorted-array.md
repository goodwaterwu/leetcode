[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

```c
/* 34. Find First and Last Position of Element in Sorted Array */
/* Given an array of integers `nums` sorted in non-decreasing order,
   find the starting and ending position of a given target value.
   If the target is not found in the array, return [-1, -1].
   The algorithm must run in O(log n) time complexity. */

/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* searchRange(int* nums, int numsSize, int target, int* returnSize) {
    int i = 0;                              /* Start index for binary search */
    int j = numsSize - 1;                   /* End index for binary search */
    int *range = (int *)malloc(2 * sizeof(int));  /* Allocate memory for result */

    range[0] = -1;                          /* Default start position */
    range[1] = -1;                          /* Default end position */
    *returnSize = 2;                        /* The result array size is always 2 */

    if (numsSize == 0)
        return range;                       /* Return [-1, -1] if array is empty */

    /* First binary search — find the first occurrence of target */
    while (i <= j) {
        int m = i + (j - i) / 2;            /* Calculate middle index */

        if (nums[m] > target) {
            j = m - 1;                      /* Target is on the left side */
        } else if (nums[m] < target) {
            i = m + 1;                      /* Target is on the right side */
        } else {
            range[0] = m;                   /* Potential first position found */
            j = m - 1;                      /* Keep searching to the left */
        }
    }

    i = 0;
    j = numsSize - 1;

    /* Second binary search — find the last occurrence of target */
    while (i <= j) {
        int m = i + (j - i) / 2;            /* Calculate middle index */

        if (nums[m] > target) {
            j = m - 1;                      /* Target is on the left side */
        } else if (nums[m] < target) {
            i = m + 1;                      /* Target is on the right side */
        } else {
            range[1] = m;                   /* Potential last position found */
            i = m + 1;                      /* Keep searching to the right */
        }
    }

    return range;                           /* Return the [start, end] range */
}
```
