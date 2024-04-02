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
```c
int romanToInt(char *s)
{
    const int roman[] = { 1, 5, 10, 50, 100, 500, 1000 };
    int integer = 0;

    while (*s != '\0') {
        switch (*s) {
        case 'I':
            if (*(s + 1) == 'V' || *(s + 1) == 'X')
                integer -= roman[0];
            else
                integer += roman[0];
            break;
        case 'V':
            integer += roman[1];
            break;
        case 'X':
            if (*(s + 1) == 'L' || *(s + 1) == 'C')
                integer -= roman[2];
            else
                integer += roman[2];
            break;
        case 'L':
            integer += roman[3];
            break;
        case 'C':
            if (*(s + 1) == 'D' || *(s + 1) == 'M')
                integer -= roman[4];
            else
                integer += roman[4];
            break;
        case 'D':
            integer += roman[5];
            break;
        case 'M':
            integer += roman[6];
            break;
        }
        s++;
    }

    return integer;
}
```
