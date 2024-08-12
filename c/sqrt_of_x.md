[Sqrt(x)](https://leetcode.com/problems/sqrtx/)

```c
int mySqrt(int x) {
    int low = 0;
    int high = x;

    if (x == 0 || x == 1)
        return x;

    while (low <= high) {
        int middle = low + (high - low) / 2;
        long long int square = (long long int)middle * middle;

        if (square == x)
            return middle;

        if (square < x)
            low = middle + 1;
        else
            high = middle - 1;
    }

    return high;
}
```
