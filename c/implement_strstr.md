[Implement strStr()](https://leetcode.com/problems/implement-strstr/)

```c
bool __strStr(char *haystack, char *needle)
{
	if (strlen(haystack) < strlen(needle))
		return false;

	for (size_t i = 0; i != strlen(needle); i++) {
		if (haystack[i] != needle[i])
			return false;
	}

	return true;
}

int strStr(char *haystack, char *needle)
{
	int index = 0;

	if (needle[0] == '\0')
		return 0;

	for (size_t i = 0; i != strlen(haystack); i++) {
		if (haystack[i] == needle[0]) {
			if (__strStr(haystack + i, needle))
				return i;
		}
	}

	return -1;
}
```
