[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

```c
/* 33. Search in Rotated Sorted Array */
/* Binary search modified to handle rotation in sorted array */

int search(int* nums, int numsSize, int target) {
    int i = 0;
    int j = numsSize - 1;

    while (i <= j) {
        int m = i + (j - i) / 2; /* Middle index */

        if (nums[m] == target)
            return m; /* Found target */

        /* Left half is sorted */
        if (nums[m] >= nums[i]) {
            if (target >= nums[i] && target < nums[m])
                j = m - 1; /* Target in left half */
            else
                i = m + 1; /* Target in right half */
        } 
        /* Right half is sorted */
        else {
            if (target > nums[m] && target <= nums[j])
                i = m + 1; /* Target in right half */
            else
                j = m - 1; /* Target in left half */
        }
    }

    return -1; /* Target not found */
}
```
