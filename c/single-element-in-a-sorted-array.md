[540. Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/description/)

```c
/* 540. Single Element in a Sorted Array */
/* Given a sorted array where every element appears exactly twice except for one element 
   which appears only once, find and return that single element in O(log n) time using binary search. */

int singleNonDuplicate(int* nums, int numsSize) {
    int i = 0;                  /* Start index of search range */
    int j = numsSize - 1;       /* End index of search range */
    int ret = 0;                /* Variable to store the unique element */

    while (i <= j) {
        int m = i + (j - i) / 2;  /* Middle index */

        if (m % 2 == 0) { /* Middle index is even */
            if (m < numsSize - 1 && nums[m] == nums[m + 1]) {
                i = m + 1; /* Pair is correct on the right, move right */
            } else {
                if (m != 0 && nums[m] == nums[m - 1]) {
                    j = m - 1; /* Pair is correct on the left, move left */
                } else {
                    ret = nums[m]; /* Found the single element */
                    break;
                }
            }
        } else { /* Middle index is odd */
            if (m != 0 && nums[m] == nums[m - 1]) {
                i = m + 1; /* Pair aligned correctly, move right */
            } else {
                if (m != numsSize - 1 && nums[m] == nums[m + 1]) {
                    j = m - 1; /* Pair misaligned, move left */
                } else {
                    ret = nums[m]; /* Found the single element */
                    break;
                }
            }
        }
    }

    return ret; /* Return the unique element */
}
```
