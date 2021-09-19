[Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

```c
static char buf[10000];
static int idx;

char push(char ch)
{
	if (idx >= sizeof(buf))
		return -1;

	buf[idx] = ch;
	idx++;

	printf("push %c\n", ch);
	return ch;
}

char pop(void)
{
	if (idx <= 0)
		return -1;

	return buf[--idx];
}

void clean(void)
{
	idx = 0;
}

bool isValid(char *s)
{
	size_t length = strlen(s);
	size_t i = 0;
	bool ret = true;

	/* Reset queue. */
	clean();

	if (length % 2)
		return false;

	for (i = 0; i != length; i++) {
		if (s[i] == '(' || s[i] == '[' || s[i] == '{') {
			if (push(s[i]) == -1)
				return false;
		} else {
			char ch = pop();

			printf("pop %c\n", ch);
			switch (s[i]) {
			case ')':
					if (ch != '(')
						ret = false;
					break;
			case ']':
					if (ch != '[')
						ret = false;
					break;
			case '}':
					if (ch != '{')
						ret = false;
					break;
			}

			if (!ret)
				return false;
		}
	}

	if (idx != 0 || s[i - 1] != ')' && s[i - 1] != ']' && s[i - 1] != '}')
		ret = false;

	return ret;
}
```
