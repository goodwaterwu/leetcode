[844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/description/)

```c
/* 844. Backspace String Compare - Stack + Simulation */

typedef struct Stack {
    char *arr;        /* Dynamic array used to store stack elements */
    int capacity;     /* Maximum capacity of the stack */
    int top;          /* Index of the next insertion position (stack top) */
} stack;

stack *init(int capacity) {
    /* Initialize a stack with given capacity */
    stack *s = (stack *)malloc(sizeof(stack));

    if (s) {
        s->arr = (char *)malloc(capacity * sizeof(char));
        s->capacity = capacity;
        s->top = 0;
    }

    return s;
}

void release(stack *s) {
    /* Free memory allocated for the stack */
    if (s)
        free(s->arr);
    free(s);
}

bool push(stack *s, char ch) {
    /* Push a character onto the stack */
    if (s->top == s->capacity)
        return false;

    s->arr[s->top] = ch;
    s->top++;

    return true;
}

bool pop(stack *s, char *ch) {
    /* Pop a character from the stack */
    if (s->top == 0)
        return false;

    s->top--;
    *ch = s->arr[s->top];

    return true;
}

void backspace(char *str) {
    /* Process the string using a stack to simulate backspace operations */
    stack *s = init(201);
    int i = 0;
    int len = 0;

    /* Traverse the string and apply backspace logic */
    while (str[i] != '\0') {
        char ch = 0;

        if (str[i] == '#')
            pop(s, &ch);     /* Simulate backspace by popping stack */
        else
            push(s, str[i]); /* Store valid characters */

        i++;
    }

    /* Reconstruct the string from stack content */
    len = s->top;
    str[len] = '\0';

    while (len > 0) {
        pop(s, &str[len - 1]);
        len--;
    }

    release(s);
}

bool backspaceCompare(char* s, char* t) {
    /* Apply backspace simulation to both strings */
    backspace(s);
    backspace(t);

    /* Compare the final processed strings */
    if (!strcmp(s, t))
        return true;

    return false;
}
```
