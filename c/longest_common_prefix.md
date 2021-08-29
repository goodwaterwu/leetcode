[Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

```c
static char prefix[201] = {0};

char * longestCommonPrefix(char ** strs, int strsSize){
	size_t min_length = strlen(strs[0]);

	memset(prefix, 0, strlen(prefix));

	/* Find min string length. */
	for (int i = 1; i != strsSize; i++) {
		if (strlen(strs[i]) < min_length)
			min_length = strs[i];
	}

	/* Compare prefix. */
	for (int i = 0; i != min_length; i++) {
		int j = 0;
		char ch = strs[0][i];

		for (j = 1; j != strsSize; j++) {
			if (ch != strs[j][i])
				break;
		}

		if (j == strsSize)
			prefix[i] = ch;
		else
			break;
	}

	return prefix;
}
```
