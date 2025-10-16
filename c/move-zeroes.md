[283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)

```c
/* 283. Move Zeroes */

/* Move all 0's in the array to the end while maintaining the relative order of non-zero elements */
void moveZeroes(int* nums, int numsSize) {
    int i = 0;  /* Pointer to the position where the next non-zero element should be placed */
    int j = 1;  /* Pointer to scan through the array */

    /* Iterate through the array */
    while (j < numsSize) {
        /* If nums[i] is non-zero, both pointers move forward */
        if (nums[i] != 0) {
            i++;
            j++;
            continue;
        }

        /* If nums[j] is non-zero, swap it with nums[i] */
        if (nums[j] != 0) {
            nums[i] = nums[j];  /* Move non-zero element forward */
            nums[j] = 0;        /* Set the scanned position to zero */
            i++;                /* Move the insertion pointer forward */
        }
        j++;  /* Always move the scanning pointer forward */
    }
}
```
