[Hamming Distance](https://leetcode.com/problems/hamming-distance/)

![image](https://github.com/goodwaterwu/leetcode/blob/master/c/images/hamming_distance.png?raw=true)

```c
int hammingDistance(int x, int y)
{
	int distance = 0;
	int tmp = x ^ y;

	for (int i = 0; i != 32; i++) {
		if (tmp & 0x1)
			distance++;

		tmp >>= 1;
	}

	return distance;
}
```
