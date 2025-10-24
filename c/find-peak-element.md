[162. Find Peak Element](https://leetcode.com/problems/find-peak-element/description/)

```c
/* 162. Find Peak Element */
/* A peak element is an element that is strictly greater than its neighbors.
   Given an integer array `nums`, find a peak element and return its index.
   You may assume that `nums[-1] = nums[n] = -∞`.
   The solution must run in O(log n) time complexity. */

int findPeakElement(int* nums, int numsSize) {
    int i = 0;                  /* Start index of the search range */
    int j = numsSize - 1;       /* End index of the search range */
    int ret = 0;                /* Variable to store the peak index */

    if (numsSize == 1)
        return 0;               /* Single element is always a peak */

    while (i <= j) {
        int m = i + (j - i) / 2;  /* Middle index */

        /* Check if m is at the boundary or greater than neighbors */
        if ((m == 0 && nums[m] > nums[m + 1]) ||
            (m == numsSize - 1 && nums[m] > nums[m - 1])) {
            ret = m;            /* Boundary peak found */
            break;
        } else {
            if (nums[m] < nums[m + 1]) {
                i = m + 1;      /* Peak is on the right side */
            } else if (nums[m] < nums[m - 1]) {
                j = m - 1;      /* Peak is on the left side */
            } else {
                ret = m;        /* nums[m] is greater than both neighbors */
                break;
            }
        }
    }

    return ret; /* Return the index of a peak element */
}
```
