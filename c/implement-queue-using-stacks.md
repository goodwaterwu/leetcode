[232. Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/description/)

```c
/* 232. Implement Queue using Stacks - Two-Stack Simulation */

#define QUEUE_SIZE 100

/* Stack structure definition */
typedef struct Stack {
    int *arr;        /* Array to store stack elements */
    int capacity;    /* Maximum capacity of the stack */
    int top;         /* Index of the next free position (stack top) */
} stack;

/* Queue structure implemented using two stacks */
typedef struct {
    stack *stk1;     /* Stack used mainly for push operations */
    stack *stk2;     /* Stack used mainly for pop and peek operations */
    int capacity;    /* Maximum capacity of the queue */
} MyQueue;

/* Initialize the queue and allocate memory for two stacks */
MyQueue* myQueueCreate() {
    MyQueue *obj = (MyQueue *)malloc(sizeof(MyQueue));
    obj->stk1 = (stack *)malloc(sizeof(stack));
    obj->stk2 = (stack *)malloc(sizeof(stack));

    obj->stk1->arr = (int *)malloc(QUEUE_SIZE * sizeof(int));
    obj->stk1->capacity = QUEUE_SIZE;
    obj->stk1->top = 0;

    obj->stk2->arr = (int *)malloc(QUEUE_SIZE * sizeof(int));
    obj->stk2->capacity = QUEUE_SIZE;
    obj->stk2->top = 0;

    obj->capacity = QUEUE_SIZE;

    return obj;
}

/* Push element x to the back of queue */
void myQueuePush(MyQueue* obj, int x) {
    stack *s1 = obj->stk1;
    stack *s2 = obj->stk2;

    /* Move all elements from stack 2 back to stack 1 */
    while (s2->top > 0) {
        s2->top--;
        s1->arr[s1->top] = s2->arr[s2->top];
        s1->top++;
    }

    /* Push the new element into stack 1 */
    s1->arr[s1->top] = x;
    s1->top++;
}

/* Removes the element from the front of queue and returns it */
int myQueuePop(MyQueue* obj) {
    stack *s1 = obj->stk1;
    stack *s2 = obj->stk2;

    /* Move all elements from stack 1 to stack 2 to reverse order */
    while (s1->top > 0) {
        s1->top--;
        s2->arr[s2->top] = s1->arr[s1->top];
        s2->top++;
    }

    /* Pop the top element from stack 2, which represents queue front */
    s2->top--;
    return s2->arr[s2->top];
}

/* Get the front element of the queue */
int myQueuePeek(MyQueue* obj) {
    stack *s1 = obj->stk1;
    stack *s2 = obj->stk2;

    /* Move all elements from stack 1 to stack 2 to access front */
    while (s1->top > 0) {
        s1->top--;
        s2->arr[s2->top] = s1->arr[s1->top];
        s2->top++;
    }

    /* Return the front element without removing it */
    return s2->arr[s2->top - 1];
}

/* Returns whether the queue is empty */
bool myQueueEmpty(MyQueue* obj) {
    if (obj->stk1->top == 0 && obj->stk2->top == 0)
        return true;

    return false;
}

/* Free all allocated memory for the queue */
void myQueueFree(MyQueue* obj) {
    if (obj) {
        if (obj->stk1)
            free(obj->stk1->arr);
        free(obj->stk1);

        if (obj->stk2)
            free(obj->stk2->arr);
        free(obj->stk2);
    }
    free(obj);
}

/**
 * Your MyQueue struct will be instantiated and called as such:
 * MyQueue* obj = myQueueCreate();
 * myQueuePush(obj, x);
 * int param_2 = myQueuePop(obj);
 * int param_3 = myQueuePeek(obj);
 * bool param_4 = myQueueEmpty(obj);
 * myQueueFree(obj);
 */
```
