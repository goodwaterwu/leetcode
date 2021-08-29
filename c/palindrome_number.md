[Palindrome Number](https://leetcode.com/problems/palindrome-number/)

```c
bool isPalindrome(int x){
	char tmp[16] = {0};
	size_t length = 0;

	/* Convert to string. */
	snprintf(tmp, sizeof(tmp), "%d", x);
	length = strlen(tmp);

	/* Check palinedrome. */
	for (int i = 0; i != length / 2; i++) {
		if (tmp[i] != tmp[length - 1 - i])
			return false;
	}

	return true;
}
```
