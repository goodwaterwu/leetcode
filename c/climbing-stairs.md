[70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

```c
/* 70. Climbing Stairs */

/* Top-Down memoization */

static int tmp[46];  /* Memoization array to store results for subproblems */

int climbStairs(int n) {
    if (n == 1) {
        tmp[1] = 1;  /* Base case: only one way to climb one step */
        return 1;  
    }
    if (n == 2) {
        tmp[2] = 2;  /* Base case: two ways to climb two steps */
        return 2;  
    }

    if (tmp[n])
        return tmp[n];  /* Return cached result if already computed */

    tmp[n] = climbStairs(n - 2) + climbStairs(n - 1);  /* Recursive relation: f(n) = f(n-1) + f(n-2) */

    return tmp[n];  /* Return computed result */
}
```

```c
/* 70. Climbing Stairs */

/* Bottom-Up tabulation */

static int dp[46];  /* DP array to store results iteratively */

int climbStairs(int n) {
    if (n == 1)
        return 1;  /* Base case: only one way to climb one step */
    if (n == 2)
        return 2;  /* Base case: two ways to climb two steps */

    if (dp[1] == 0) {
        dp[1] = 1;  /* Initialize base case for step 1 */
        dp[2] = 2;  /* Initialize base case for step 2 */
    }

    for (int i = 3; i <= n; i++)
        dp[i] = dp[i - 2] + dp[i - 1];  /* Iterative relation: f(i) = f(i-1) + f(i-2) */

    return dp[n];  /* Return the final result */
}
```

```c
/* 70. Climbing Stairs */

/* Bottom-Up constant space */

int climbStairs(int n) {
    if (n == 1)
        return 1;  /* Base case: only one way to climb one step */
    if (n == 2)
        return 2;  /* Base case: two ways to climb two steps */

    int prev = 1;  /* f(n-2) */
    int curr = 2;  /* f(n-1) */
    int ret = 0;   /* f(n) */

    for (int i = 3; i <= n; i++) {
        ret = prev + curr;  /* Compute current step count */
        prev = curr;        /* Shift prev forward */
        curr = ret;         /* Shift curr forward */
    }

    return ret;  /* Return the total number of ways */
}
```
