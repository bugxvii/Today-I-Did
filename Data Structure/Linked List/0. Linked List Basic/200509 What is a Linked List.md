tags: #linkedlist #data-structure #english

<hr />

[[200509 연결 리스트(Linked List)란 | 🇰🇷 한국어]]
[[200509 連結リスト(Linked List)とは | 🇯🇵 日本語]]

## Linked List

A **linked list** is a data structure which stores the object in **linear order**.

This order, however, is not decided by its index like an array. The order of the linked list is determined by a pointer in each object.

![linkedlist](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/637ddad6-f0c7-47df-b785-fd6591e7b74f/linkedlist.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052834Z&X-Amz-Expires=86400&X-Amz-Signature=24d1f33e76b81324d99db19542d74bdcd6312d21280e0aca41782f1c2e382370&X-Amz-SignedHeaders=host)

## Node

Each object in a list is called **node**.

Node consists of a _data_ and a pointer that references the _next_, _previous_, or _both_.

```cpp
class Node 
{
  public: 
    Node(int val):data(val), next(nullptr), prev(nullptr) {}

    int data;
    Node *next;
    Node *prev;
};
```

## Types of Linked List

-   Singly
    -   node has a _next_ pointer.
-   Doubly
    -   node has both _next_ and _prev_ pointers.
-   Circular
    -   the first node's _prev_ points to the last node and last node's _tail_ points to the first node.
-   Sorted
    -   singly, doubly, or circular linked list with orders preserved.
    -   The head node is the smallest item and the tail node is the largest or vice versa.

## Operations

### search(L, k)

This function finds the first element with key _k_ in list _L_.

```cpp
Node* search(Node *L, int key) 
{
  Node *curr = L->head;
  while (curr->next != nullptr and curr->key != key)
    curr = curr->next;

  return curr;
}
```

Time complexity: **O(n)**

### insert(L, x)

This function splices `x` onto the front of the list `L`.

```cpp
  void insert(Node *L, Node *x) 
  {
    x->next = L->head;
    if (L->head != nullptr)
      L->head->prev = x;

    L->head = x;
    x->prev = nullptr;
  }
```

Time complexity: **O(1)**

### delete(L, x)

This function removes an element `x` from the list `L`.

```cpp
  void delete(Node *L, Node *x) 
  {
    if (x->prev != nullptr)
      x->prev->next = x->next;
    else
      L->head = x->next;

    if (x->next != nullptr)
      x->next->prev = x->prev;

    delete x;
  }
```

Time complexity: **O(1)**

## Sentinels

We can ignore the boundary conditions of head and tail in `insert` and `delete` by using a **sentinel** node.

A _sentinel_ is simply a dummy node that lies in between head and tail and it doesn't hold any values.

`sentinel->next` points to the head and `sentinel->prev` points to the tail of the list.

![sentinels](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9c60e716-0d80-44d6-82f4-1f1d84920375/sentinel-node.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052834Z&X-Amz-Expires=86400&X-Amz-Signature=3f307c77d869a672831f10a84dcfe1ba541f332205699eb66d328242e26ce9fa&X-Amz-SignedHeaders=host) 
img src: Introduction to Algorithms, 3rd Edition (CLRS)

Part `(a)` shows an **empty** list with only the sentinel in the list.

In part `(b)`, `sentinel->next` points to the first node of the list (`9`) and `sentinel->prev` points to the last node of the list(`1`).

Now we can simplify our `insert` and `delete` function like the below.

```cpp
 void insert(Node *sentinel, Node *x) 
 {
   x->next = sentinel->next;
   sentinel->next->prev = x;
   sentinel->next = x;
   x->prev = sentinel;
 }

 void delete(Node *x) 
 {
   x->prev->next = x->next;
   x->next->prev = x->prev;
   delete x;
 }
```

Sentinels should be used judiciously since it doesn't have any effect on its performance (it takes away the O(1) opertaion so reduces the coefficient but it doesn't change the complexity).

In fact, it could waste lot of memory by adding an extra node, a sentinel, in many small lists. So use sentinels when you're sure that it will simplify your code.

## Advantages of Linked List
-   Size is dynamic. The size of the list will grow and shrink as we insert or delete a node.
-   Linked lists have faster insert and delete operations.

## Disadvantages of Linked List
-   Random access is not allowed. We have to access elements sequentially starting from the first node.
-   Every time we create a new node, we're using that much more memory.
-   Array elements are located contiguously in a memory so there's locality of reference. But elements in linked lists are not; thus, linked lists are not cache friendly.

| Operation | Array | Linked List |
|------|------|-----------|
|  Access  |  O(1) | O(n) |
| Search | O(n) | O(n) |
| Insert | O(n) | O(1) |
| Delete | O(n) | O(1) |


## Reference
-   Introduction to Algorithms, 3rd Edition (CLRS)
