[Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

```c
int minSubArrayLen(int target, int *nums, int numsSize) {
    int i = 0;
    int sum = 0;
    int min = numsSize + 1;

    /* Sliding window */
    for (int j = 0; j != numsSize; j++) {
        int len = numsSize;

        sum += nums[j];
        while (sum >= target) {
            len = j - i + 1; /* Window size */
            min = (min < len) ? min : len; /* Minimum window size */
            sum -= nums[i++];
        }
    }

    return (min > numsSize) ? 0 : min;
}
```
