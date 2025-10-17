[217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/description/)

```c
/* 217. Contains Duplicate */

#include <stdlib.h>
#include <stdbool.h>

/* Comparison function for qsort */
int compare(const void *a, const void *b) {
    return (*(int *)a - *(int *)b);
}

/* Determine if the array contains any duplicates */
bool containsDuplicate(int* nums, int numsSize) {
    int i = 0;  /* Iterator for traversing the sorted array */

    /* If there is only one element, duplicates are impossible */
    if (numsSize == 1)
        return false;

    /* Sort the array to bring duplicates together */
    qsort(nums, numsSize, sizeof(int), compare);

    /* Check adjacent elements for duplicates */
    while (i < numsSize - 1) {
        if (nums[i] == nums[i + 1])
            return true;  /* Duplicate found */
        i++;
    }

    return false;  /* No duplicates found */
}
```
