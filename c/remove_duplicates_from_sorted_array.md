[Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

```c
int removeDuplicates(int* nums, int numsSize)
{
	int count = 0;

	if (numsSize <= 1)
		return numsSize;

	count++;
	for (int i = 0; i != numsSize - 1; i++) {
		if (nums[i] != nums[i + 1])
			nums[count++] = nums[i + 1];
	}

	return count;
}
```
