[Mode Zeroes](https://leetcode.com/problems/move-zeroes/)

```c
void moveZeroes(int* nums, int numsSize) {
    int index = 0; /* The new array index */

    /* i means the original array index */
    for (int i = 0; i != numsSize; i++) {
        if (nums[i] != 0) {
            int tmp = nums[index];

            nums[index++] = nums[i];
            nums[i] = tmp;
        }
    }
}
```
