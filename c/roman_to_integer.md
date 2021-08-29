[Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

```c
int romanToInt(char * s){
	int ret = 0;

	for (int i = 0; i != strlen(s); i++) {
		switch (s[i]) {
		case 'M':
				ret += 1000;
				break;
		case 'D':
				ret += 500;
				break;
		case 'C':
				if (s[i + 1] == 'D') {
					ret += 400;
					i++;
				} else if (s[i + 1] == 'M') {
					ret += 900;
					i++;
				} else {
					ret += 100;
				}
				break;
		case 'L':
				ret += 50;
				break;
		case 'X':
				if (s[i + 1] == 'L') {
					ret += 40;
					i++;
				} else if (s[i + 1] == 'C') {
					ret += 90;
					i++;
				} else {
					ret += 10;
				}
				break;
		case 'V':
				ret += 5;
				break;
		case 'I':
				if (s[i + 1] == 'V') {
					ret += 4;
					i++;
				} else if (s[i + 1] == 'X') {
					ret += 9;
					i++;
				} else {
					ret++;
				}
				break;
		}
	}

	return ret;
}
```
