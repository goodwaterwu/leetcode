[Valid Perfect Square](https://leetcode.com/problems/valid-perfect-square/)

```c
bool isPerfectSquare(int num) {
    int low = 0;
    int high = num;

    if (num == 1)
        return true;

    while (low <= high) {
        int middle = low + (high - low) / 2;
        long long int square = (long long int)middle * middle;

        if (square == num)
            return true;

        if (square < num)
            low = middle + 1;
        else
            high = middle - 1;
    }

    return false;
}
```
