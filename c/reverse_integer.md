[Reverse Integer](https://leetcode.com/problems/reverse-integer/)

```c
int reverse(int x)
{
	size_t length = 0;
	long int tmp = 0;
	int ret = 0;
	char origin[16] = {0};
	char after[16] = {0};

	/* Convert integer to string. */
	if (x >= 0)
		snprintf(origin, sizeof(origin), "%ld", (long int)x);
	else
		snprintf(origin, sizeof(origin), "%ld", -((long int)x));

	length = strlen(origin);

	/* Reverse string. */
	for (int i = length - 1; i >= 0; i--)
		after[length - 1 - i] = origin[i];

	/* Convert string back to integer. */
	tmp = strtol(after, NULL, 10);

	/* Check overflow. */
	ret = (int)tmp;
	if (tmp - ret)
		return 0;

	if (x < 0)
		ret = -ret;

	return ret;
}
```
