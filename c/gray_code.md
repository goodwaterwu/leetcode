[Gray Code](https://leetcode.com/problems/gray-code/)

![image](https://github.com/goodwaterwu/leetcode/blob/master/c/images/gray_code.png?raw=true)

```c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* grayCode(int n, int *returnSize)
{
	int *gray = NULL;
	int index = 0;

	*returnSize = 1 << n;
	gray = malloc(*returnSize * sizeof(int));
	if (!gray)
		return NULL;

	gray[index++] = 0;

	/* If n = 0, size = 1 and gray array is [0] */
	if (n == 0) {
		*returnSize = 1;
		return gray;
	}

	for (int i = 1; i != *returnSize; i++) {
		/*
		 * If i is odd, toggle rightmost bit
		 * If i is even, toggle the left bit of first bit = 1
		 */
		if (i & 0x1) {
			gray[index++] = gray[index - 1] ^ 0x1;
		} else {
			for (int j = 0; j != n; j++) {
				if ((gray[index - 1] >> j) % 2) {
					gray[index++] = gray[index - 1] ^ (1 << (j + 1));
					break;
				}
			}
		}
	}

	return gray;
}
```
