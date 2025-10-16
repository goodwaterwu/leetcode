[27. Remove Element](https://leetcode.com/problems/remove-element/description/)

```c
/* 27. Remove Element */
int removeElement(int* nums, int numsSize, int val) {
    int i = 0;  /* Pointer for the position to insert the next valid element */
    int j = 0;  /* Pointer for scanning through the array */

    /* Iterate through the entire array */
    while (j < numsSize) {
        /* If the current element is NOT equal to the value to remove */
        if (nums[j] != val) {
            nums[i] = nums[j];  /* Copy the valid element to the front */
            i++;                /* Move the insert pointer forward */
        }
        j++;  /* Always move the scan pointer forward */
    }

    /* Return the new length of the array after removing all 'val' elements */
    return i;
}
```
