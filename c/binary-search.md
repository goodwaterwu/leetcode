[704. Binary Search](https://leetcode.com/problems/binary-search/description/)

```c
/* 704. Binary Search */

int search(int* nums, int numsSize, int target) {
    /* Initialize left pointer to the first index */
    int i = 0;

    /* Initialize right pointer to the last index */
    int j = numsSize - 1;

    /* Continue searching while the valid search range exists */
    while (i <= j) {

        /* 
         * Calculate the middle index safely to avoid integer overflow.
         * This is equivalent to (i + j) / 2, but safer.
         */
        int middle = i + (j - i) / 2;

        /* If middle value is smaller than target, discard left half */
        if (nums[middle] < target)
            i = middle + 1;

        /* If middle value is larger than target, discard right half */
        else if (nums[middle] > target)
            j = middle - 1;

        /* Target found, return its index */
        else
            return middle;
    }

    /* Target not found, return -1 */
    return -1;
}
```
