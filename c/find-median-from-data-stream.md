[295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/description/)

```c
/* 295. Find Median from Data Stream */

/* 
 * Heap structure used for both min-heap and max-heap.
 * arr      : dynamically allocated array storing heap elements
 * capacity : maximum number of elements the heap can hold
 * size     : current number of elements in the heap
 */
typedef struct Heap {
    int *arr;
    int capacity;
    int size;
} heap;

/*
 * MedianFinder structure.
 * min_heap : min-heap storing the larger half of the numbers
 * max_heap : max-heap storing the smaller half of the numbers
 * size     : total number of elements added so far
 * median_index : unused helper array (kept unchanged)
 */
typedef struct {
    heap *min_heap;
    heap *max_heap;
    int size;
    int median_index[2];
} MedianFinder;

/*
 * Initialize a heap with the given capacity.
 * Memory is allocated for both the heap structure and its internal array.
 */
heap *init(int capacity) {
    heap *h = (heap *)malloc(sizeof(heap));

    if (h) {
        h->arr = (int *)calloc(capacity, sizeof(int));
        h->capacity = capacity;
        h->size = 0;
    }

    return h;
}

/*
 * Free all memory associated with a heap.
 */
void release(heap *h) {
    if (h->arr)
        free(h->arr);
    free(h);
}

/*
 * Swap two integer values in memory.
 * Used extensively during heap operations.
 */
void swap(int *a, int *b) {
    int tmp = *a;
    *a = *b;
    *b = tmp;
}

/*
 * Restore the min-heap property by moving the element at index i upward.
 * This is called after inserting a new element.
 */
void minheap_heapify_up(heap *h, int i) {
    while (i > 0 && h->arr[i] < h->arr[(i - 1) / 2]) {
        swap(&h->arr[i], &h->arr[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}

/*
 * Restore the min-heap property by moving the element at index i downward.
 * This is called after removing the root element.
 */
void minheap_heapify_down(heap *h, int i) {
    int min = i;

    while (1) {
        int left = i * 2 + 1;
        int right = i * 2 + 2;

        /* Find the smallest among current node and its children */
        if (left < h->size && h->arr[min] > h->arr[left])
            min = left;
        if (right < h->size && h->arr[min] > h->arr[right])
            min = right;

        /* If the current node is already the smallest, stop */
        if (min == i)
            break;

        swap(&h->arr[i], &h->arr[min]);
        i = min;
    }
}

/*
 * Restore the max-heap property by moving the element at index i upward.
 */
void maxheap_heapify_up(heap *h, int i) {
    while (i > 0 && h->arr[i] > h->arr[(i - 1) / 2]) {
        swap(&h->arr[i], &h->arr[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}

/*
 * Restore the max-heap property by moving the element at index i downward.
 */
void maxheap_heapify_down(heap *h, int i) {
    int max = i;

    while (1) {
        int left = i * 2 + 1;
        int right = i * 2 + 2;

        /* Find the largest among current node and its children */
        if (left < h->size && h->arr[max] < h->arr[left])
            max = left;
        if (right < h->size && h->arr[max] < h->arr[right])
            max = right;

        /* If the current node is already the largest, stop */
        if (max == i)
            break;

        swap(&h->arr[i], &h->arr[max]);
        i = max;
    }
}

/*
 * Insert a value into the min-heap.
 * Returns false if the heap is already full.
 */
bool minheap_push(heap *h, int num) {
    if (h->size == h->capacity)
        return false;

    h->arr[h->size] = num;
    minheap_heapify_up(h, h->size);
    h->size++;

    return true;
}

/*
 * Remove and return the smallest element from the min-heap.
 */
bool minheap_pop(heap *h, int *num) {
    if (h->size == 0)
        return false;

    h->size--;
    *num = h->arr[0];
    h->arr[0] = h->arr[h->size];
    minheap_heapify_down(h, 0);

    return true;
}

/*
 * Insert a value into the max-heap.
 */
bool maxheap_push(heap *h, int num) {
    if (h->size == h->capacity)
        return false;

    h->arr[h->size] = num;
    maxheap_heapify_up(h, h->size);
    h->size++;

    return true;
}

/*
 * Remove and return the largest element from the max-heap.
 */
bool maxheap_pop(heap *h, int *num) {
    if (h->size == 0)
        return false;

    h->size--;
    *num = h->arr[0];
    h->arr[0] = h->arr[h->size];
    maxheap_heapify_down(h, 0);

    return true;
}

/*
 * Create and initialize a MedianFinder object.
 * Two heaps are used:
 * - max-heap for the smaller half of numbers
 * - min-heap for the larger half of numbers
 */
MedianFinder* medianFinderCreate() {
    MedianFinder *obj = (MedianFinder *)calloc(1, sizeof(MedianFinder));
    obj->min_heap = init(25000);
    obj->max_heap = init(25000);

    return obj;
}

/*
 * Add a number into the MedianFinder.
 * The number is first inserted into the appropriate heap,
 * then the heaps are rebalanced to maintain size constraints.
 */
void medianFinderAddNum(MedianFinder* obj, int num) {
    obj->size++;

    /* Decide which heap should store the new number */
    if (obj->max_heap->size == 0 || num <= obj->max_heap->arr[0])
        maxheap_push(obj->max_heap, num);
    else
        minheap_push(obj->min_heap, num);

    /* Ensure max-heap has at most one more element than min-heap */
    if (obj->max_heap->size - obj->min_heap->size >= 2) {
        int n = 0;
        maxheap_pop(obj->max_heap, &n);
        minheap_push(obj->min_heap, n);
    }

    /* Ensure min-heap never has more elements than max-heap */
    if (obj->min_heap->size > obj->max_heap->size) {
        int n = 0;
        minheap_pop(obj->min_heap, &n);
        maxheap_push(obj->max_heap, n);
    }
}

/*
 * Return the median of all inserted numbers.
 * - If total count is odd, the median is the root of the max-heap.
 * - If total count is even, the median is the average of both heap roots.
 */
double medianFinderFindMedian(MedianFinder* obj) {
    double median = 0.0;

    if (obj->size % 2)
        median = obj->max_heap->arr[0];
    else
        median = (obj->min_heap->arr[0] + obj->max_heap->arr[0]) / 2.0;

    return median;
}

/*
 * Free all memory associated with the MedianFinder.
 */
void medianFinderFree(MedianFinder* obj) {
    if (obj->min_heap)
        release(obj->min_heap);
    if (obj->max_heap)
        release(obj->max_heap);
    free(obj);
}

/**
 * Your MedianFinder struct will be instantiated and called as such:
 * MedianFinder* obj = medianFinderCreate();
 * medianFinderAddNum(obj, num);
 * double param_2 = medianFinderFindMedian(obj);
 * medianFinderFree(obj);
 */
```
