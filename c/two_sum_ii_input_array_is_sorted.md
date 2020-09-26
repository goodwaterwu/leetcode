[Two Sum II - Input array is sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

![image](https://github.com/goodwaterwu/leetcode/blob/master/c/images/two_sum_ii_input_array_is_sorted.png?raw=true)

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* twoSum(int* numbers, int numbersSize, int target, int* returnSize) {
	int i = 0;
	int j = numbersSize - 1;
	int *answer = calloc(sizeof(int), 2);

	if (!answer)
		return NULL;

	while (1) {
		int sum = *(numbers + i) + *(numbers + j);

		if (sum == target) {
			*(answer + 0) = i + 1;
			*(answer + 1) = j + 1;
			*returnSize = 2;
			break;
		} else if (sum < target) {
			i++;
		} else {
			j--;
		}
	}

	return answer;
}
```
