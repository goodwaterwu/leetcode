[Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)

```c
void getTypedString(char *str) {
    int index = 0; /* The new array index */

    /* The original array index */
    for (int i = 0; str[i] != 0; i++) {
        if (str[i] == '#') {
            index = (index > 0) ? (index - 1) : 0;
            str[index] = 0; /* Do backspace action */
            str[i] = 0; /* Clean finished characters */
        } else {
            if (index != i) {
                str[index] = str[i]; /* Update value if needed */
                str[i] = 0; /* Clean finished characters */
            }
            index++;
        }
    }
}

bool backspaceCompare(char *s, char *t) {
    getTypedString(s);
    getTypedString(t);
    if (strcmp(s, t) == 0)
        return true;

    return false;
}
```
