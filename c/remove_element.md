[Remove Element](https://leetcode.com/problems/remove-element/)

```c
int removeElement(int *nums, int numsSize, int val)
{
	int count = 0;

	for (int i = 0; i != numsSize; i++) {
		if (nums[i] != val)
			nums[count++] = nums[i];
	}

	return count;
}
```
```c
int removeElement(int *nums, int numsSize, int val)
{
    int count = 0;

    if (val > 50)
        return numsSize;

    if (numsSize == 0)
        return 0;

    if (numsSize == 1)
        return (nums[0] == val) ? 0 : 1;

    if (nums[0] == val) {
        if (nums[numsSize - 1] != val) {
            nums[0] = nums[numsSize - 1];
            count += removeElement(nums + 1, numsSize - 2, val) + 1;
        } else {
            count += removeElement(nums, numsSize - 1, val);
        }
    } else {
        count += removeElement(nums + 1, numsSize - 1, val) + 1;
    }

    return count;
}
```
