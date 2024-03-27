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
```c
int majorityElement(int *nums, int numsSize)
{
    // Boyer–Moore majority vote algorithm
    int candidate = nums[0];
    int vote = 1;

    for (int i = 1; i != numsSize; i++) {
        if (candidate == nums[i]) {
            vote++;
        } else {
            if (vote == 0)
                candidate = nums[i];
            else
                vote--;
        }
    }

    return candidate;
}
```
