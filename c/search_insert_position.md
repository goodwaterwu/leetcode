[Search Insert Position](https://leetcode.com/problems/search-insert-position/)

```c
int searchInsert(int *nums, int numsSize, int target)
{
	int lower = 1;
	int upper = numsSize;
	int index = 0;
	int ret = 0;
	bool found = false;

	if (numsSize <= 0 || nums[0] > target)
		return 0;

	if (nums[numsSize - 1] < target)
		return numsSize;

	if (numsSize == 1) {
		if (nums[0] <= target)
			return 0;
		else
			return 1;
	}

	do {
		index = (lower + upper) / 2;
		if (nums[index - 1] < target) {
			if (index <= numsSize) {
				if (nums[index] >= target) {
					ret = index;
					found = true;
				} else {
					lower = index;
				}
			} else {
				lower = index;
			}
		} else {
			upper = index;
		}

		if (lower == upper) {
			ret = index - 1;
			found = true;
		}
	} while (!found);

	return ret;
}
```
