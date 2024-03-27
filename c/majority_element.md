[Majority Element](https://leetcode.com/problems/majority-element)

```c
#include <stdlib.h>

int compare(const void *a, const void *b)
{
    return (*(int*)b - *(int*)a);
}

int majorityElement(int *nums, int numsSize)
{
    // The majority is in the middle of the sorted array.
    qsort(nums, numsSize, sizeof(int), compare);

    return nums[numsSize / 2];
}
```
