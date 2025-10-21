[148. Sort List](https://leetcode.com/problems/sort-list/description/)

```c
/* 148. Sort List */

/* Definition for singly-linked list */
/* struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */

/* Define a MinHeap structure to store pointers to ListNode */
typedef struct MinHeap {
    struct ListNode **nodes; /* Array of pointers to ListNode */
    int capacity;            /* Maximum capacity of the heap */
    int size;                /* Current number of elements in the heap */
} heap;

/* Initialize a heap with given capacity */
heap *init(int capacity) {
    heap *h = (heap *)malloc(sizeof(heap));

    if (h) {
        h->nodes = (struct ListNode **)malloc(capacity * sizeof(struct ListNode *)); /* Allocate memory for node pointers */
        h->capacity = capacity;  /* Set heap capacity */
        h->size = 0;             /* Initialize heap size to 0 */
    }

    return h;
}

/* Reinitialize a heap with a new capacity (resize) */
heap *reinit(heap *h, int capacity) {
    if (h) {
        h->nodes = (struct ListNode **)realloc(h->nodes, capacity * sizeof(struct ListNode *)); /* Resize array */
        h->capacity = capacity; /* Update capacity */
    } else {
        h = init(capacity); /* If heap is NULL, create new heap */
    }

    return h;
}

/* Release memory allocated for the heap */
void release(heap *h) {
    if (h) {
        if (h->nodes)
            free(h->nodes); /* Free the array of node pointers */
        free(h);            /* Free heap structure */
    }
}

/* Move the node at index i up to maintain min-heap property */
void heapify_up(heap *h, int i) {
    while (1) {
        if (i == 0 || h->nodes[i]->val > h->nodes[(i - 1) / 2]->val)
            break;

        struct ListNode *tmp = h->nodes[i];               /* Swap with parent if smaller */
        h->nodes[i] = h->nodes[(i - 1) / 2];
        h->nodes[(i - 1) / 2] = tmp;
        i = (i - 1) / 2;                                  /* Move to parent's index */
    }
}

/* Insert a node into the heap */
bool push(heap *h, struct ListNode *node) {
    if (h->size == h->capacity)
        return false;            /* Heap is full */

    h->nodes[h->size] = node;    /* Place node at the end */
    heapify_up(h, h->size);      /* Restore min-heap property */
    h->size++;                    /* Increase heap size */

    return true;
}

/* Move the node at index i down to maintain min-heap property */
void heapify_down(heap *h, int i) {
    while (1) {
        int smallest = i;
        int left = 2 * i + 1;     /* Left child index */
        int right = 2 * i + 2;    /* Right child index */

        if (left < h->size) {
            if (h->nodes[left]->val < h->nodes[smallest]->val)
                smallest = left;
        }
        if (right < h->size) {
            if (h->nodes[right]->val < h->nodes[smallest]->val)
                smallest = right;
        }
        if (smallest == i)
            break;

        struct ListNode *tmp = h->nodes[i]; /* Swap with smaller child */
        h->nodes[i] = h->nodes[smallest];
        h->nodes[smallest] = tmp;
        i = smallest;                       /* Move to child's index */
    }
}

/* Remove and return the smallest node from the heap */
bool pop(heap *h, struct ListNode **node) {
    if (h->size == 0)
        return false;               /* Heap is empty */

    *node = h->nodes[0];            /* Store root node */
    h->size--;                       /* Decrease heap size */
    h->nodes[0] = h->nodes[h->size];/* Move last node to root */
    heapify_down(h, 0);              /* Restore min-heap property */

    return true;
}

/* Sort a linked list using min-heap */
struct ListNode* sortList(struct ListNode* head) {
    if (!head)
        return NULL;                 /* Empty list */

    struct ListNode *tmp = head;
    heap *h = init(1);               /* Initialize heap with capacity 1 */

    while (tmp) {                     /* Push all nodes into heap */
        if (h->size == h->capacity) {
            int capacity = h->capacity * 2; /* Double capacity if full */
            h = reinit(h, capacity);
        }
        push(h, tmp);
        tmp = tmp->next;
    }

    struct ListNode *tmp2 = NULL;
    pop(h, &tmp);                     /* Pop smallest node as new head */
    head = tmp;
    tmp2 = head;
    while (pop(h, &tmp)) {            /* Pop remaining nodes in order */
        tmp2->next = tmp;
        tmp2 = tmp2->next;
    }

    tmp2->next = NULL;                 /* Terminate sorted list */
    release(h);                        /* Free heap memory */

    return head;
}
```
