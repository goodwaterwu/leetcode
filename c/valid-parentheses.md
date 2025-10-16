[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)

```c
/* 20. Valid Parentheses */

/* Stack structure to store parentheses */
typedef struct Stack {
    char *parentheses;  /* Array to hold parentheses characters */
    int capacity;       /* Maximum capacity of the stack */
    int top;            /* Index of the top element in the stack */
} stack;

/* Initialize a stack with a given capacity */
stack *init(int capacity) {
    stack *s = (stack *)malloc(sizeof(stack));

    if (s) {
        s->parentheses = (char *)malloc(capacity * sizeof(char)); /* Allocate memory for elements */
        s->capacity = capacity;                                   /* Set stack capacity */
        s->top = 0;                                               /* Initialize top index */
    }

    return s;  /* Return pointer to the stack */
}

/* Release memory allocated for the stack */
void release(stack *s) {
    if (s) {
        if (s->parentheses)
            free(s->parentheses);  /* Free the element array */
        free(s);                    /* Free the stack structure */
    }
}

/* Push a character onto the stack */
bool push(stack *s, char c) {
    if (s->top == s->capacity)
        return false;  /* Stack overflow */

    s->parentheses[s->top] = c;  /* Add character to stack */
    s->top++;                     /* Move top index forward */

    return true;                  /* Push successful */
}

/* Pop a character from the stack */
bool pop(stack *s, char *c) {
    if (s->top == 0)
        return false;  /* Stack underflow */

    s->top--;                    /* Move top index backward */
    *c = s->parentheses[s->top]; /* Retrieve character */

    return true;                 /* Pop successful */
}

/* Check if the input string has valid parentheses */
bool isValid(char* s) {
    stack *st = init(strlen(s));  /* Initialize stack with string length */
    int i = 0;                     /* Index for iterating through the string */
    bool ret = true;               /* Result flag */

    /* Iterate through each character in the string */
    while (s[i]) {
        /* Push opening parentheses onto the stack */
        if (s[i] == '(' || s[i] == '{' || s[i] == '[') {
            push(st, s[i]);
        } else {
            char c;
            /* Pop from stack; if stack is empty then invalid */
            if (!pop(st, &c)) {
                ret = false;
                goto early_return;
            }

            /* Check if the popped character matches the closing parenthesis */
            if (s[i] == ')' && c != '(' ||
                s[i] == '}' && c != '{' ||
                s[i] == ']' && c != '[') {
                ret = false;
                goto early_return;
            }
        }
        i++;
    }

    /* If stack is not empty at the end, parentheses are unmatched */
    if (st->top != 0)
        ret = false;

early_return:
    release(st);  /* Release allocated memory */

    return ret;   /* Return whether the string is valid */
}
```
