[287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/description/)

```c
/* 287. Find the Duplicate Number */

typedef struct MinHeap {
    int *arr;
    int capacity;
    int size;
} heap;

/* Initialize a min-heap with given capacity */
heap *init(int capacity) {
    heap *h = (heap *)malloc(sizeof(heap));

    if (h) {
        /* Allocate array for heap elements */
        h->arr = (int *)malloc(capacity * sizeof(int));
        h->capacity = capacity;
        h->size = 0;
    }

    return h;
}

/* Release memory allocated for heap */
void release(heap *h) {
    if (h)
        free(h->arr);

    free(h);
}

/* Swap two integers */
void swap(int *a, int *b) {
    int tmp = *a;

    *a = *b;
    *b = tmp;
}

/* Restore heap property by bubbling up */
void heapify_up(heap *h, int i) {
    while (i > 0 && h->arr[i] < h->arr[(i - 1) / 2]) {
        swap(&h->arr[i], &h->arr[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}

/* Restore heap property by bubbling down */
void heapify_down(heap *h, int i) {
    int smallest = i;

    while (1) {
        int left = i * 2 + 1;
        int right = i * 2 + 2;

        /* Find smallest among node and children */
        if (left < h->size && h->arr[smallest] > h->arr[left])
            smallest = left;

        if (right < h->size && h->arr[smallest] > h->arr[right])
            smallest = right;

        /* If child is smaller, swap and continue */
        if (smallest != i) {
            swap(&h->arr[i], &h->arr[smallest]);
            i = smallest;
        } else {
            break;
        }
    }
}

/* Insert a value into the heap */
bool push(heap *h, int value) {
    if (h->size >= h->capacity)
        return false;

    h->arr[h->size] = value;
    heapify_up(h, h->size);
    h->size++;

    return true;
}

/* Remove smallest value from heap */
bool pop(heap *h, int *value) {
    if (h->size == 0)
        return false;

    *value = h->arr[0];
    h->arr[0] = h->arr[h->size - 1];
    h->size--;
    heapify_down(h, 0);

    return true;
}

/* Find the duplicate number by sorting via min-heap */
int findDuplicate(int* nums, int numsSize) {
    heap *h = init(numsSize);
    int previous = -1;

    /* Push all numbers into heap */
    for (int i = 0; i < numsSize; i++)
        push(h, nums[i]);

    /* Pop numbers and check for duplicate */
    for (int i = 0; i < numsSize; i++) {
        int value = 0;

        pop(h, &value);
        if (previous == value) {
            release(h);
            return value;
        }

        previous = value;
    }

    release(h);
    return -1;
}
```

```c
/* 287. Find the Duplicate Number */
/* Floyd's Cycle Detection (Tortoise and Hare Algorithm) */

int findDuplicate(int* nums, int numsSize) {
    /* Slow pointer (tortoise) */
    int i = 0;
    /* Fast pointer (hare) */
    int j = 0;

    /* Phase 1: Detect cycle using Floyd's Cycle Detection */
    while (1) {
        /* Move slow pointer by one step */
        i = nums[i];
        /* Move fast pointer by two steps */
        j = nums[nums[j]];
        /* Meeting point indicates a cycle exists */
        if (i == j)
            break;
    }

    /* Phase 2: Find the entry point of the cycle */
    j = 0;
    while (1) {
        /* Move both pointers one step at a time */
        i = nums[i];
        j = nums[j];
        /* The meeting point is the duplicate number */
        if (i == j)
            break;
    }

    /* Return the duplicate number */
    return i;
}
```
