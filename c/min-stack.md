[155. Min Stack](https://leetcode.com/problems/min-stack/description/)

```c
/* 155. Min Stack */

typedef struct {
    /* Stack to store values */
    int *arr;
    /* Stack to store minimum values at each level */
    int *min;
    /* Maximum stack size */
    int size;
    /* Current top index */
    int top;
} MinStack;

/* Create and initialize a MinStack */
MinStack* minStackCreate() {
    /* Allocate memory for stack structure */
    MinStack *s = (MinStack *)malloc(sizeof(MinStack));
    s->size = 30000;
    /* Initialize top to 0 (empty stack) */
    s->top = 0;
    /* Allocate memory for value stack */
    s->arr = (int *)malloc(s->size * sizeof(int));
    /* Allocate memory for minimum stack */
    s->min = (int *)malloc(s->size * sizeof(int));

    return s;
}

/* Push a value onto the stack */
void minStackPush(MinStack* obj, int val) {
    /* Store the value */
    obj->arr[obj->top] = val;

    /* If it's the first element or val is smaller than previous min, update min */
    if (obj->top == 0 || val < obj->min[obj->top - 1])
        obj->min[obj->top] = val;
    else
        /* Otherwise, inherit the previous minimum */
        obj->min[obj->top] = obj->min[obj->top - 1];

    /* Move top pointer up */
    obj->top++;
}

/* Remove the top element */
void minStackPop(MinStack* obj) {
    /* Decrease top pointer */
    obj->top--;
}

/* Return the top element of the stack */
int minStackTop(MinStack* obj) {
    return obj->arr[obj->top - 1];
}

/* Return the minimum element in the stack */
int minStackGetMin(MinStack* obj) {
    return obj->min[obj->top - 1];
}

/* Free all allocated memory */
void minStackFree(MinStack* obj) {
    if (obj) {
        /* Free value stack */
        if (obj->arr)
            free(obj->arr);

        /* Free minimum stack */
        if (obj->min)
            free(obj->min);
    }
    /* Free the stack object */
    free(obj);
}

/*
 * Your MinStack struct will be instantiated and called as such:
 * 
 * MinStack* obj = minStackCreate();
 * minStackPush(obj, val);
 * minStackPop(obj);
 * int param_3 = minStackTop(obj);
 * int param_4 = minStackGetMin(obj);
 * minStackFree(obj);
 */
```
