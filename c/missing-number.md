[268. Missing Number](https://leetcode.com/problems/missing-number/description/)

```c
/* 268. Missing Number */

#include <stdlib.h>
#include <stdbool.h>

/* Find the missing number in an array containing n distinct numbers in the range [0, n] */
int missingNumber(int* nums, int numsSize) {
    int i = 0;
    /* Allocate a boolean array to mark which numbers are present */
    bool *found = (bool *)calloc(numsSize + 1, sizeof(bool));

    /* Mark each number in the array as found */
    while (i < numsSize) {
        found[nums[i]] = true;
        i++;
    }

    i = 0;
    /* Find the first number that was not found */
    while (i < numsSize + 1) {
        if (!found[i])
            break;
        i++;
    }

    free(found);  /* Free allocated memory */

    return i;  /* Return the missing number */
}
```
