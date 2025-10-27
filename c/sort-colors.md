[75. Sort Colors](https://leetcode.com/problems/sort-colors/description/)

```c
/* 75. Sort Colors */
/* Given an array nums with n objects colored red (0), white (1), or blue (2),
   sort them in-place so that objects of the same color are adjacent,
   with the colors in the order red, white, and blue. */

void sortColors(int* nums, int numsSize) {
    int count[3] = {0};   /* Counters for 0s, 1s, and 2s */
    int i = 0;

    /* Count occurrences of each color */
    while (i < numsSize) {
        switch (nums[i]) {
            case 0:
                count[0]++;
                break;
            case 1:
                count[1]++;
                break;
            case 2:
                count[2]++;
                break;
        }
        i++;
    }

    /* Overwrite nums array based on counts */
    i = 0;
    while (i < numsSize && count[0] > 0) {
        nums[i++] = 0;
        count[0]--;
    }
    while (i < numsSize && count[1] > 0) {
        nums[i++] = 1;
        count[1]--;
    }
    while (i < numsSize && count[2] > 0) {
        nums[i++] = 2;
        count[2]--;
    }
}
```
