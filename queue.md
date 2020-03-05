```c
typedef struct {
    int front;
    int rear;
    int size;
    int data[0];
} MyCircularQueue;

/** Initialize your data structure here. Set the size of the queue to be k. */
/** Checks whether the circular queue is empty or not. */
bool myCircularQueueIsEmpty(MyCircularQueue* obj) {
    return (obj->front == -1);
}

/** Checks whether the circular queue is full or not. */
bool myCircularQueueIsFull(MyCircularQueue* obj) {
    return (obj->rear + 1) % obj->size == obj->front;  
}

MyCircularQueue* myCircularQueueCreate(int k) {
    if (k == 0) {
        return NULL;
    }
    MyCircularQueue *que = calloc(1, sizeof(*que) + k *sizeof(int));
    if (que == NULL) {
        return NULL;
    }
    que->front = que->rear = -1;
    que->size = k;
    return que;
}

/** Insert an element into the circular queue. Return true if the operation is successful. */
bool myCircularQueueEnQueue(MyCircularQueue* obj, int value) {
    if (obj == NULL || myCircularQueueIsFull(obj)) {
        return false;
    }
    if (obj->front == -1) {
        obj->front = 0;
    }
    obj->rear = (obj->rear + 1) % obj->size;
    obj->data[obj->rear] = value;
    return true;
}

/** Delete an element from the circular queue. Return true if the operation is successful. */
bool myCircularQueueDeQueue(MyCircularQueue* obj) {
    if (obj == NULL || myCircularQueueIsEmpty(obj)) {
        return false;
    }
    if (obj->front == obj->rear) {
        obj->front = obj->rear = -1;
        return true;
    }
    obj->front = (obj->front + 1) % obj->size;
    return true;
}

/** Get the front item from the queue. */
int myCircularQueueFront(MyCircularQueue* obj) {
    if (obj == NULL || myCircularQueueIsEmpty(obj)) {
        return -1;
    }
    return obj->data[obj->front];
}

/** Get the last item from the queue. */
int myCircularQueueRear(MyCircularQueue* obj) {
    if (obj == NULL || myCircularQueueIsEmpty(obj)) {
        return -1;
    }
    return obj->data[obj->rear];  
}

void myCircularQueueFree(MyCircularQueue* obj) {
    free(obj);
}

```
