tags: #dll #linkedlist #data-structure #english 

<hr />

[[200711 이중 연결 리스트(Doubly Linked List)란 | 🇰🇷 한국어]]
[[200711 双方向連結リスト(Doubly Linked List)とは | 🇯🇵 日本語]]

## Doubly Linked List

Doubly Linked List is a linear data structure where each node contains two pointers: `prev` and `next`.

`next` pointer is used to reference the node one next to the current node. `prev` is from the word _preivous_;

`B->prev` refers to the node one previous to `B`, which is `A` in the figure below.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3484b447-1446-4b29-8bae-9e7db88a9a49/dll.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=6830acbd11940d8f751c0fde906b69187bd64e3365acd553aeb83f3cbc0b52d9&X-Amz-SignedHeaders=host)

## structure of a node

As I mentioned above, a node contains two pointers in doubly list, `prev` and `next`.

```cpp
template <class T>
class Node 
{ 
  private:
  public:
    Node<T>(T val) : prev(nullptr), next(nullptr) { data = val; }
    Node<T> *prev;
    Node<T> *next;
    T data;
};
```

In singly list, we were only able to move in one direction; in doubly list, however, we can traverse a list in either directions using these two pointers.

## implementation

Here's the specification of the doubly linked list we are going to implement at this post.

```cpp
template <class T>
class DoublyLinkedList 
{
  private: 
    Node<T> *head;
    int capacity;

  public: 
    DoublyLinkedList(int val);
    ~DoublyLinkedList();

    void init(T val);
    void insert_back(int val);
    void insert_front(int val);
    void insert_at(int index, int val);

    void remove_back();
    void remove_front();
    void remove_at(int index);

    void link(Node<T> *a, Node<T> *b);
    void print();
};
```

Let's go through each member functions and see how it's implemented.

## constructor

```cpp
template <class T>
DoublyLinkedList<T>::DoublyLinkedList(int val)
{
  head = new Node<T>(val);
  tail = head;
  head->next = tail;
  tail->prev = head;
  head->prev = tail->next = nullptr;
}
```

This constructor takes an argument and initializes the list with a node, which is `head`.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c85274ce-2bb3-4435-9394-b2c8cf14d47e/sll-constructor-1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=bc5960531f62dcc1c808689757a1e579c1b31b68751d651d0a50fe4510c7b239&X-Amz-SignedHeaders=host)

## inserting a node

I'll be using the helper function called `link(curr, newNode)`.

```cpp
template <class T>
void DoublyLinkedList<T>::link(Node<T> *curr, Node<T> *newNode)
{
  curr->next = newNode;
  newNode->prev = curr;
}
```

### insert\_back

```cpp
template <class T>
void DoublyLinkedList<T>::insert_back(int val) 
{
  Node<T> *newNode = new Node(val);
  if (capacity == 1)
  {
    link(head, newNode);
  }
  else 
  {
    link(tail, newNode);
  }
  tail = newNode;
}
```

Keep in mind that I'm using two nodes, `head` and `tail`.

When the list contains a singly node, the `head`, we link a `newNode` with `head`. This is the first `if` condition.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c32ce2f9-a64a-4006-be10-1f3c4886db82/dll-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=0d200517f12c1551a35b63ba4160d711f274d0e452b3830cbee2965b06ee40a2&X-Amz-SignedHeaders=host)

When the list contains more than one node, we simply connect the `tail` with the `newNode`. This is the `else` part.

Then, we update the tail.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5bdb3025-2546-4f0a-bc4b-026f007ffb5b/dll-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=39f81cb2fdb21d36d9867978253f5b1704d0f23348497a2108b133e32c0139b9&X-Amz-SignedHeaders=host)

### insert\_front

```cpp
template <class T>
void DoublyLinkedList<T>::insert_front(int val) 
{
  Node<T> *newNode = new Node(val);
  if (capacity == 1)
  {
    link(newNode, tail);
  }
  else
  {
    link(newNode, head);
  }
  head = newNode;
}
```

The `insert_front` works exactly the same as the `insert_back`. We just change the operation done on `head` to `tail` and vice versa. And update the `head` to `newNode` instead of the `tail`.

### insert\_at

We can insert a new node in between two nodes using the `insert_at` function.

Parameters are `index`, a position of a node to insert, and `val`, a data for a node to hold. The index is **zero-based**.

```cpp
template <class T>
void DoublyLinkedList<T>::insert_at(int index, int val) 
{
  if (index <= 0) 
  {
    insert_front(val);
  }
  else if (index >= capacity) 
  {
    insert_back(val);
  }
  else 
  {
    Node<T> *temp = head;
    for (int i=0; i<index; ++i) 
    {
      temp = temp->next;
    }

    Node<T> *newNode = new Node(val);
    temp->prev->next = newNode;
    newNode->prev = temp->prev;
    link(newNode, temp);
  }
}
```

I handled following errors, _negative index_ and _index out bounds_, by simply calling functions we implemented earlier:`insert_front(..)` and `insert_back(..)`

Now let's look at the case where we're actually inserting a node in between two nodes.

First, we navigate to the node positioned at `index`.

```cpp
  Node<T> *temp = head;
  for (int i=0; i<index; ++i) 
  {
    temp = temp->next;
  }
```

So if `index = 1`, we will be at the second element (**B**) in the list like the figure below.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef15c6aa-59b1-426a-a2ac-07329daae763/dll-insert_at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=c8e0326275fb5807d9762ec6e55828d22ae3e7ecb8cbea67cfa6cde08a29abe2&X-Amz-SignedHeaders=host)

Now connect `newNode` with a node in previous of `temp`.

```cpp
  temp->prev->next = newNode;
  newNode->prev = temp->prev;
```

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/65987769-29ab-4e64-84f2-9ff30ce24c07/dll-insert_at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=76d5d3d35cfab176e3b73d463e73421ef57bb5134d8506bc1458d8edeee13f81&X-Amz-SignedHeaders=host)

And finally connect `newNode` with `temp` so that it is placed at the `index`.

```cpp
  link(newNode, temp);
```

![dll](https://eubug.space/_next/image?url=https%3A%2F%2Fapi.super.so%2Fasset%2Feubug.space%2Fbb83bd03-5791-4e16-9ae2-81922f51eda6.png&w=1920&q=100)

And we're done. This figure above, however, looks very messy so lets clean it up, and you'll see clearly that the `newNode` is placed at the `index`.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2decd4ea-098e-4aa3-b50e-e14f54964dcf/dll-insert_at4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=b9e6b0772b22755cfe10c2bce0130dd42317f889c8f0a3d089b4b0d38f3efb86&X-Amz-SignedHeaders=host)

## removing a node

### remove\_back

```cpp
template <class T>
void DoublyLinkedList<T>::remove_back()
{
  if (capacity == 1)
  {
    delete head;
    head = tail = nullptr;
    capacity = 0;
  }
  else
  {
    Node<T> *temp = tail;
    tail = tail->prev;
    delete temp;
    tail->next = nullptr;

    --capacity;
  }
}
```

Let's suppose that we have a list like the below and we're trying remove the tail.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/535954ee-8558-4dd8-be3f-b570019458fd/dll-remove1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=a09b52465a9be94cf979ab8833d841a18d32dd131c66506a1afb384051c407ef&X-Amz-SignedHeaders=host)

It's actually very easy. We just move the `tail` to its previous, `tail->prev`, and delete the old tail.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3123385-7579-4f38-a2e1-3b21a3a25f06/dll-remove2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=96b13d12df034d79d35581bf4af306bc927e9a096bb0532fce0f42c539f29e80&X-Amz-SignedHeaders=host)

### remove\_front

```cpp
template <class T>
void DoublyLinkedList<T>::remove_front()
{
  if (capacity == 1)
  {
    delete head;
    head = tail = nullptr;
    capacity = 0;
  }
  else
  {
    Node<T> *temp = head;
    head = head->next;
    delete temp;
    head->prev = nullptr;

    --capacity;
  }
}
```

This one is exactly same as the above except that we're working with the `head` not the `tail`.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ebebbf76-ce03-40a9-a4d8-27c1209233a2/dll-remove3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=f0b8e232b15f74af442509c1a379adb0b028946f2fb9d12d593f1ca0b744e242&X-Amz-SignedHeaders=host)

### remove\_at

```cpp
template <class T>
void DoublyLinkedList<T>::remove_at(int index)
{
  if (index <= 0) 
    remove_front();
  else if (index >= (capacity-1)) 
    remove_back();
  else 
  {
    Node<T> *temp = head;
    for(int i=0; i<index; ++i) 
    {
      temp = temp->next;
    }

    temp->prev->next = temp->next;
    temp->next->prev = temp->prev;
    delete temp;
  }
}
```

Let's assume that we have a list like the following and we're trying to delete the middle element, _data_.

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/27d53126-e94a-4b90-8b4e-e30386f6a6d4/dll-remove1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=68e104cb809c53254b51cf27626c6dc38a7ea53e08bab43d9b663648fed66f36&X-Amz-SignedHeaders=host)

We first navigate to that node we're trying to delete.

```cpp
  Node<T> *temp = head;
  for(int i=0; i<index; ++i) 
  {
    temp = temp->next;
  }
```

Then delete its node after re-linking its `prev` and `next`.

```cpp
  temp->prev->next = temp->next;
  temp->next->prev = temp->prev;
  delete temp;
```

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9fecf7ac-9e05-4d9c-b960-39f7daf1f39f/dll-remove_at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=b25d13b7b02ccf25d45690122090d5930f941d24daef0b96b3e1eb357c6668d3&X-Amz-SignedHeaders=host)

## view full code
- https://github.com/eubug17/ds-algo/blob/master/linkedlist/doubly/dll.hpp