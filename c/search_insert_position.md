[Search Insert Position](https://leetcode.com/problems/search-insert-position/)

```c
int searchInsert(int *nums, int numsSize, int target)
{
    int low = 0;
    int high = numsSize - 1;

    while (low <= high) {
        int middle = low + (high - low) / 2;

        if (nums[middle] < target)
            low = middle + 1;
        else
            high = middle - 1;
    }

    return high + 1;
}
```
