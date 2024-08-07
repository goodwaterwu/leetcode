[Binary Search](https://leetcode.com/problems/binary-search/)

```c
int search(int* nums, int numsSize, int target) {
    int low = 0;
    int high = numsSize - 1;

    while (low <= high) {
        int middle = low + (high - low) / 2;

        if (nums[middle] == target)
            return middle;

        if (nums[middle] < target)
            low = middle + 1;
        else
            high = middle - 1;
    }

    return -1;
}
```
