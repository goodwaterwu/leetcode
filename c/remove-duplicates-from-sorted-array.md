[26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

```c
/* 26. Remove Duplicates from Sorted Array */

/* Remove duplicates in-place from a sorted array and return the new length */
int removeDuplicates(int* nums, int numsSize) {
    int i = 0;         /* Pointer for the position to insert the next unique element */
    int j = 1;         /* Pointer for scanning through the array */

    /* Iterate through the array */
    while (j < numsSize) {
        if (nums[i] != nums[j]) {   /* Found a new unique element */
            i++;
            nums[i] = nums[j];      /* Move it to the correct position */
        }
        j++;
    }

    return i + 1;   /* New length of the array with unique elements */
}
```
