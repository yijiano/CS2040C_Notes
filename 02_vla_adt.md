#cs2040c #vla #adt

[[_main|<-- Back to main]]

# Abstract Data Types
- Stack
- List
- Queue

## Symbol Table #symbol_table
Interface/behaviour:
```c
void insert(Key k, Value v);
void search(Key k;
void delete(Key k);
bool contains(Key k);
int size();
```

# Stack #stack
#LIFO (Last-In, First-out)
Implementation:
```c
void push(T x); // top of the stack is also the head
T pop(); // removes and returns top element
bool empty();
```

# Queue #queue
#FIFO (First-In, First-out)
Implementation:
```c
void enqueue(T x); // front of queue is the head
T dequeue(); // removes and returns the end element
bool empty();
```

# List #list
Implementation:
```c
void append(T x); // add to end of list
void prepend(T x); // add to start of list
void insert(T x, int slot);
void remove(T x);
T getFirst();
T getLast();
T get(int slot);
bool isEmpty();
```
