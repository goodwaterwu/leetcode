[202. Happy Number](https://leetcode.com/problems/happy-number/description/)

```c
/* 202. Happy Number */
int help(int n) {
    /* Variable to store the sum of squares of digits */
    int sum = 0;

    /* Calculate the sum of squares of each digit */
    while (n > 0) {
        sum += (n % 10) * (n % 10);
        n /= 10;
    }

    /* Return the computed sum */
    return sum;
}

bool isHappy(int n) {
    /* Slow pointer initialized to n */
    int i = n;

    /* Fast pointer initialized to the result of one transformation */
    int j = help(n);

    /* Use Floyd's cycle detection to find a loop */
    while (i != j) {
        i = help(i);
        j = help(help(j));
    }

    /* If the cycle ends at 1, the number is happy */
    return (i == 1);
}
```

```c
/* 202. Happy Number */
bool isHappy(int n) {
    /* Variable to store the sum of squares of digits */
    unsigned long long int sum = 0;

    /* Repeat the process until the result is determined */
    while (1) {
        /* Extract digits and accumulate the square of each digit */
        if (n > 0) {
            sum += (n % 10) * (n % 10);
            n /= 10;
            continue;
        }

        /* If the sum is a single digit but not 1 or 7, it is not a happy number */
        if (sum < 10 && sum != 1 && sum != 7)
            return false;

        /* If the sum becomes 1, the number is happy */
        if (sum == 1)
            break;

        /* Continue the process with the new sum */
        n = sum;
        sum = 0;
    }

    /* Return true if the number is happy */
    return true;
}
```
