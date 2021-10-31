[Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

```c
int maxSubArray(int *nums, int numsSize)
{
	int max = nums[0];

	if (numsSize == 1)
		return nums[0];

	for (int i = 1; i != numsSize; i++) {
		/*
		 * Set nums[i] equals to the result of
		 * previous i - 1 or nums[i]
		 */
		if (nums[i - 1] + nums[i] > nums[i])
			nums[i] = nums[i - 1] + nums[i];
	}

	for (int i = 1; i != numsSize; i++) {
		if (max < nums[i])
			max = nums[i];
	}

	return max;
}
```
