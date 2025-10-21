[215. Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

```c
/* 215. Kth Largest Element in an Array */

/* Define a structure for MinHeap */
typedef struct MinHeap {
    int *arr;        /* Array to store heap elements */
    int capacity;    /* Maximum capacity of the heap */
    int size;        /* Current number of elements in the heap */
} heap;

/* Initialize a heap with given capacity */
heap *init(int capacity) {
    heap *h = (heap *)malloc(sizeof(heap));

    if (h) {
        h->arr = (int *)malloc(capacity * sizeof(int)); /* Allocate memory for heap array */
        h->capacity = capacity;                          /* Set heap capacity */
        h->size = 0;                                     /* Initialize heap size to 0 */
    }

    return h;
}

/* Release memory allocated for the heap */
void release(heap *h) {
    if (h) {
        if (h->arr)
            free(h->arr);   /* Free the array inside heap */
        free(h);             /* Free the heap structure */
    }
}

/* Swap two integers */
void swap(int *a, int *b) {
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

/* Move the element at index i up to maintain min-heap property */
void heapify_up(heap *h, int i) {
    while (1) {
        if (i == 0 || h->arr[i] > h->arr[(i - 1) / 2])
            break;
        swap(&h->arr[i], &h->arr[(i - 1) / 2]); /* Swap with parent if smaller */
        i = (i - 1) / 2;                        /* Move to parent's index */
    }
}

/* Insert a value into the heap */
bool push(heap *h, int val) {
    if (h->size == h->capacity)
        return false;  /* Heap is full */

    h->arr[h->size] = val;          /* Place new value at the end */
    heapify_up(h, h->size);         /* Restore min-heap property */
    h->size++;                       /* Increase heap size */

    return true;
}

/* Move the element at index i down to maintain min-heap property */
void heapify_down(heap *h, int i) {
    while (1) {
        int smallest = i;
        int left = 2 * i + 1;      /* Left child index */
        int right = 2 * i + 2;     /* Right child index */

        if (left < h->size) {
            if (h->arr[left] < h->arr[smallest])
                smallest = left;
        }
        if (right < h->size) {
            if (h->arr[right] < h->arr[smallest])
                smallest = right;
        }

        if (smallest == i)
            break;

        swap(&h->arr[i], &h->arr[smallest]); /* Swap with smaller child */
        i = smallest;                         /* Move to child's index */
    }
}

/* Remove and return the smallest element from the heap */
bool pop(heap *h, int *val) {
    if (h->size == 0)
        return false;        /* Heap is empty */

    *val = h->arr[0];        /* Store the root value */
    h->size--;               /* Decrease heap size */
    h->arr[0] = h->arr[h->size]; /* Move last element to root */
    heapify_down(h, 0);      /* Restore min-heap property */

    return true;
}

/* Get the smallest element without removing it */
bool peek(heap *h, int *val) {
    if (h->size == 0)
        return false;        /* Heap is empty */

    *val = h->arr[0];        /* Return root value */

    return true;
}

/* Find the k-th largest element in an array using min-heap of size k */
int findKthLargest(int* nums, int numsSize, int k) {
    int i = 1;
    int val = 0;
    heap *h = init(k);        /* Initialize min-heap with capacity k */

    push(h, nums[0]);         /* Push first element into heap */
    while (i < numsSize) {
        if (i < k) {
            push(h, nums[i]); /* Fill heap with first k elements */
        } else {
            peek(h, &val);    /* Get current smallest in heap */
            if (nums[i] > val) { /* If new element is bigger than min */
                pop(h, &val);    /* Remove smallest */
                push(h, nums[i]); /* Insert new element */
            }
        }
        i++;
    }

    peek(h, &val);            /* The root of heap is the k-th largest element */
    release(h);               /* Free heap memory */

    return val;
}
```
