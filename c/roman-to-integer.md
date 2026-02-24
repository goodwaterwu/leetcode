[13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/description/)

```c
/* 13. Roman to Integer - Greedy + Simulation */

int roman_value(char c) {
    /* Convert a single Roman numeral character to its integer value */
    int val = 0;

    switch (c) {
        case 'I':
            val = 1;
            break;
        case 'V':
            val = 5;
            break;
        case 'X':
            val = 10;
            break;
        case 'L':
            val = 50;
            break;
        case 'C':
            val = 100;
            break;
        case 'D':
            val = 500;
            break;
        case 'M':
            val = 1000;
            break;
        default:
            break;
    }

    return val;
}

int romanToInt(char* s) {
    /* Accumulator for the final integer result */
    int sum = 0;
    int i = 0;

    /* Traverse the Roman numeral string */
    while (i < strlen(s)) {
        int curr = roman_value(s[i]);
        int next = roman_value(s[i + 1]);

        /* If a smaller value appears before a larger one, subtract it */
        if (curr != '\0' && curr < next)
            sum -= curr;
        else
            sum += curr;

        i++;
    }

    /* Return the converted integer value */
    return sum;
}
```
