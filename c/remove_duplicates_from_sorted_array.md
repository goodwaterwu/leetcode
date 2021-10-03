[Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

```c
int removeDuplicates(int* nums, int numsSize) {
    int index = 1; /* The new array index */

    /* i means the index to be removed or moved */
    for (int i = 1; i != numsSize; i++) {
        if (nums[i] != nums[i - 1])
            nums[index++] = nums[i];
    }

    return index;
}
```
