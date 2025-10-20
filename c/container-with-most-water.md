[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/description/)

```c
/* 11. Container With Most Water */

/* Find the maximum area of water that can be contained */
int maxArea(int* height, int heightSize) {
    int i = 0;                  /* Left pointer */
    int j = heightSize - 1;     /* Right pointer */
    int max = 0;                /* Maximum area found */

    /* Two-pointer approach */
    while (i < j) {
        int w = j - i;                              /* Width between pointers */
        int h = (height[i] < height[j]) ? height[i] : height[j];  /* Min height */
        int area = w * h;                            /* Current area */

        if (area > max)
            max = area;                              /* Update max if larger */

        /* Move the pointer pointing to the shorter line */
        if (height[i] < height[j])
            i++;
        else
            j--;
    }

    return max;
}

```
