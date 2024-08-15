[Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

```c
int totalFruit(int *fruits, int fruitsSize) {
    int i = 0;
    int max = 0;
    int len = 0;
    int baskets[2] = {-1, -1}; /* baskets for putting fruits */
    int lasts[2] = {-1, -1}; /* Last index of fruit in baskets  */

    if (fruitsSize == 1)
        return 1;

    /* Sliding window */
    for (int j = 0; j != fruitsSize; j++) {
        if (baskets[0] == fruits[j]) {
            lasts[0] = j; /* Update last index of the first fruit */
        } else if (baskets[1] == fruits[j]) {
            lasts[1] = j; /* Update last index of the second fruit */
        } else {
            if (baskets[0] == -1) { /* The first basket is empty */
                baskets[0] = fruits[j];
                lasts[0] = j;
            } else if (baskets[1] == -1) { /* The second basket is empty */
                baskets[1] = fruits[j];
                lasts[1] = j;
            } else {
                if (lasts[0] < lasts[1]) {
                    i = lasts[0] + 1; /* The first index of the second fruit */
                    baskets[0] = fruits[j]; /* Change fruit in the first basket */
                    lasts[0] = j; /* Update the last index of the first fruit */
                } else {
                    i = lasts[1] + 1; /* The first index of the first fruit */
                    baskets[1] = fruits[j]; /* Change fruit in the second basket */
                    lasts[1] = j; /* Update the last index of the second fruit */
                }
            }
        }

        len = j - i + 1;
        max = (max < len) ? len : max;
    }

    return max;
}
```
