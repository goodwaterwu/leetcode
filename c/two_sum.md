[Two Sum](https://leetcode.com/problems/two-sum/)

![image](https://github.com/goodwaterwu/leetcode/blob/master/c/images/two_sum.png?raw=true)

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int *twoSum(int *nums, int numsSize, int target, int *returnSize)
{
	int i = 0;
	int j = 0;
	int *answer = calloc(sizeof(int), 2);

	if (!answer)
		return NULL;

	for (i = 0; i != numsSize - 1; i++) {
		for (j = i + 1; j != numsSize; j++) {
			if (*(nums + i) + *(nums + j) == target) {
				*(answer + 0) = i;
				*(answer + 1) = j;
				*returnSize = 2;
				return answer;
			}
		}
	}

	return answer;
}
```
