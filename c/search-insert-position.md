[35. Search Insert Position](https://leetcode.com/problems/search-insert-position/description/)

```c
/* 35. Search Insert Position */
/* Given a sorted array 'nums' and a 'target', return the index if the target is found. 
   If not, return the index where it would be inserted in order. */

int searchInsert(int* nums, int numsSize, int target) {
    int i = 0;                /* Start of search range */
    int j = numsSize - 1;     /* End of search range */
    int candidate = 0;        /* Candidate insertion index */

    /* If target is greater than the last element, it should be inserted at the end */
    if (target > nums[numsSize - 1])
        return numsSize;

    while (i <= j) {
        int m = i + (j - i) / 2; /* Middle index to avoid overflow */

        /* For debugging: print current indices and candidate */
        if (nums[m] < target) {
            i = m + 1;          /* Search in the right half */
        } else if (nums[m] > target) {
            candidate = m;      /* Update candidate for insertion */
            j = m - 1;          /* Search in the left half */
        } else {
            return m;           /* Target found at index m */
        }
    }

    /* Return the index where the target should be inserted */
    return candidate;
}
```
