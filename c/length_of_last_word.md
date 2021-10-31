[Length of Last Word](https://leetcode.com/problems/length-of-last-word/)

```c
int lengthOfLastWord(char *s)
{
	char *token = strtok(s, " ");
	char *last = NULL;

	while (token) {
		last = token;
		token = strtok(NULL, " ");
	}

	if (last)
		return strlen(last);

	return 0;
}
```
