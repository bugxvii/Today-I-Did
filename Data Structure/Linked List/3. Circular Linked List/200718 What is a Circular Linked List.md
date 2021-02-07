tags: #cll #linkedlist #data-structure #english 

<hr />

[[200718 원형 연결 리스트(Circular Linked List)란 | 🇰🇷 한국어]]
[[200718 循環リスト(Circular Linked List)とは | 🇯🇵 日本語]]

## Circular Linked List

In **Singly** and **Doubly Linked List**, we can track the end of list by finding a node that points to `nil`; doubly linked has one more of this node, which is `head.prev` like the figure below.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7c3a7a09-5151-4ca1-9920-fa54d7af6190/cll-doubly-example.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=a712ad3436c81e74219e9215b856d576318df8fe63a394ccc515b9a6b6436262&X-Amz-SignedHeaders=host)

A circular list is a linked list that does not end; there is no `nll`. The last element of the node links back to its first node;

for the case of a doubly linked list, `head.prev`is linked with the last node. This is perhaps why it's called a _circular_ linked list.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fe881d2f-26ab-4836-851f-484157291e3a/cll-doubly.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=d1c3dd39524e1960464055c46690e4aaff30e27ce7fe97915dd8286e175e1a0c&X-Amz-SignedHeaders=host)

## Structure of a Node

A circular linked list is a variation of a singly and a doubly linked list, thus the structure of a node in a circular list will be based on the type of a linked list we use.

### circular singly linked list

```cpp
template <class T>
class Node 
{ 
  private:
  public:
    Node<T>(T val) : next(nullptr) { data = val; }
    Node<T> *next;
    T data;
};
```

### circular doubly linked list

```cpp
template <class T>
class Node 
{ 
  private:
  public:
    Node<T>(T val) : next(nullptr), prev(nullptr) { data = val; }
    Node<T> *next;
    Node<T> *prev;
    T data;
};
```

## Implementation

Here's the skeleton of a circular linked list we're going to implement. For the full source code, please refer to the link at the Reference section.

```cpp
template <class T>
class CircularLinkedList 
{
  private:
    // ...
  public: 
    CircularLinkedList(T val);
    ~CircularLinkedList();

    void insert_front(T val);
    void insert_back(T val);

    void remove_front();
    void remove_back();

    // ...
};
```

## Constructor

### circular singly linked list

In a singly linked list, most operations start by accessing the first node and traverse to insert, delete, or search an element.

So we save the first element into a node called `head` or `first` (names don't matter, but these two are typically used).

Circular singly linked list is little different. We save the _last_ element into a node called `tail` or `last`; we don't use `head`.

```cpp
template <class T>
CircularLinkedList<T>::CircularLinkedList(int val)
{
  last = new Node(val);
  last->next = last;
  size = 1;
}
```

Having the `last` node serves as a great advantage in singly linked lists especially when inserting a new element at the end.

We don't have to traverse the whole list; we can insert a new element at the end in constant time using `last->next`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/707a65bc-567f-4a04-a497-c24b4ce2e048/cll-singly-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=305994d70dccc4905054c5c079ac7850a4639d24a2a862701de17824c2d4039d&X-Amz-SignedHeaders=host)

### circular doubly linked list

A doubly linked list can traverse the list in both ways using `next` and `prev` pointers, thus there's no need to use the `last` node.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bcfbe732-5e91-42a6-8e3d-08795bff08ed/cll-doubly-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=28721274fe759b4051d987b0e81eb6c1c32322abf45dbad2ee8d9a8dd943effb&X-Amz-SignedHeaders=host)

We use `head` and access the last node via `head->prev`.

```cpp
template <class T>
DoublyLinkedList<T>::DoublyLinkedList(int val)
{
  head = new Node(val);
  head->next = head->prev = head;
  size = 1;
}
```

## Insert at the beginning

### circular singly linked list

```cpp
template <class T>
void CircularSinglyLinkedList<T>::insert_front(int val) 
{
  Node<T> *newNode = new Node(val);
  newNode->next = last->next;
  last->next = newNode;
}
```

We need to let `newNode` point to the first element in the list which is `last->next`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6acda366-905c-4ffa-b11d-dd069eff9731/cll-singly-insert_at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=631e7463099a0eabaec2da62dea4cb1de1b61eacc68ec3d8db84e1dd96063b99&X-Amz-SignedHeaders=host)

Currently our `last->next` is pointing at A. We need to update this so that it's pointing at the new head, which is `newNode`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3a44e82-aeea-4eee-b883-eb11b9a17e45/cll-singly-insert_at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=e3e2ef46850d32a994ea02510f432b5dffe47a4519c26324dc4d71d654a965c0&X-Amz-SignedHeaders=host)

### circular doubly linked list

```cpp
template <class T>
void CircularDoublyLinkedList<T>::insert_front(int val) 
{
  Node<T> *newNode = new Node(val);

  newNode->next = head;
  newNode->prev = head->prev;
  head->prev->next = newNode;
  head->prev = newNode;
  head = newNode;
}
```

First connect `newNode->prev` and `newNode->next`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/be260084-0a88-456e-84f4-6c4cfe3efb5f/cll-doubly-insert_at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=745d7adca491994926acfd41c2d0c9c7ec0eec663eb096ca407af57774024cff&X-Amz-SignedHeaders=host)

Our current `last->next` is pointing at the first element in the list. Update this so that its pointing at `newNode`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c83c6e1a-080e-4f9f-ac1d-08212b817ee5/cll-doubly-insert_at4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=16fb6d24e92a47c2cc1d11eeae7912a9189c8c735b254b69d751ab097d111935&X-Amz-SignedHeaders=host)

And lastly, update our current `head->prev` so that it points to `newNode`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f44c4c8-d1e8-4aef-ad81-a759ffddd03d/cll-doubly-insert_at5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=36cbb861dca222d25fe9271db968b39fc200a8b80e06985d2296dab7dbab9aad&X-Amz-SignedHeaders=host)

## Insert at the end

### circular singly linked list

At the beginning of this post, I mentioned that it's easier to insert an element at the end when we use the `tail` node. This is the part.

Here's the code.

```cpp
template <class T>
void CircularSinglyLinkedList<T>::insert_back(int val) 
{
  Node<T> *newNode = new Node(val);
  newNode->next = last->next;
  last->next = newNode;
  last = newNode;
}
```

`newNode` is going to be our new last, thus `newNode->next` should point to the first element of the list, which is current `last->next`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ed7152f6-bbf6-492c-83e9-57f5a07f0a2e/cll-singly-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=ab12e861c0bc13f2e7760c48586c5287d4fb8c7da851ee4ab0e3c9748b099801&X-Amz-SignedHeaders=host)

Now change the link for `last->next` so that its pointing `newNode`, which is our new last. And update `last`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f5d38300-468b-457b-857b-f3c467ee9efb/cll-singly-insert3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=8f753092b95037876b12b9794e45c1bace6060aa2f10d4f884fdc2944851359c&X-Amz-SignedHeaders=host)

### circular doubly linked list

```cpp
template <class T>
void CircularDoublyLinkedList<T>::insert_back(int val) 
{
  Node<T> *newNode = new Node(val);

  Node<T> *last = head->prev;
  newNode->prev = last;
  newNode->next = head;
  last->next = newNode;
  head->prev = newNode;
}
```

Let's connect `newNode->prev` and `newNode->next` with current last and first node respectively.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dbae4da0-b1ab-493e-8483-ab0fc7b79b5f/cll-doubly-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=1d322032a0a5722c7cd31cc339c7f36bc5eea6c31b0ff919c3a1f25c7e5b3dd6&X-Amz-SignedHeaders=host)

Our current `last`, which is B, is pointing at the first element. Re-link this node and let it point to `newNode`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c05c3d51-4b43-4dee-a6f6-f89f85224c14/cll-doubly-insert3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=075d02782fe0745c43d8a4de923946f38cd6ef22ab4e8b5800993f8af8206189&X-Amz-SignedHeaders=host)

Last but not least, the previous node of our current `head` should now be the `newNode`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b2f1c9a-769f-41fd-8457-32f2b9a71bb5/cll-doubly-insert4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=1ca4cf0498d1eac18afe4dcb5a10eda39fe1ede4da46e37321f207305fdf8a39&X-Amz-SignedHeaders=host)

## Remove the first node

### circular singly linked list

```cpp
template <class T>
void CircularSinglyLinkedList<T>::remove_front()
{
  Node<T> *temp = last->next;
  last->next = last->next->next;

  delete temp;
}
```

The process of removing the first node is candid. Since `last->next` is pointing at the first node, we just update this link.

Assume we have a list with three elements like the below.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2a61b93d-0230-4c6c-9e26-acc583d92467/cll-singly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=6d241f1c322643ae169cc80dfcc8f15eed75697e0369f5ea75a8cd0af435cd0c&X-Amz-SignedHeaders=host)

We can let our `last->next` point it its next which is `last->next->next`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9e7558f7-6888-4712-aca3-c512281866ac/cll-doubly-remove-at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=228579d333485e553e1c0b6d3e1f841da04fb6c0c4f5fa8a7cc12131065e71b2&X-Amz-SignedHeaders=host)

### circular doubly linked list

```cpp
template <class T>
void CircularDoublyLinkedList<T>::remove_front()
{
  Node<T> *temp = head->next;
  head->next->prev = head->prev;
  head->prev->next = head->next;
  delete head;
  head = temp;
}
```

This one is also very straightforward. Perhaps, it's easier than the circular singly list.

Given a list like the below, let's remove the head node.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2c497d36-9238-4097-b2c3-f392188b5dd3/cll-doubly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=c6091e9bf8b3afb866f9657e1430152479d67de0dce5dacf39e289247725db90&X-Amz-SignedHeaders=host)

First, delink all nodes connected to `head`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a92b0e2f-8b95-4014-9e85-86b3c8e66a97/cll-doubly-remove-at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=dbba6f106a44f8d03359ba6604187ef0a94b8b95e8bd4c000c88883fdbb96a3c&X-Amz-SignedHeaders=host)

And update the `head` and we're done.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/183d9e0e-8552-449f-b153-c840def10f2a/cll-doubly-remove-at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=3caca4f5e321aa35a9c586f9f0913a8fbf129ccae4a8ce3b9e5ca8ef7167f017&X-Amz-SignedHeaders=host)

## Remove the last node

### circular singly linked list

```cpp
template <class T>
void CircularSinglyLinkedList<T>::remove_back()
{
  Node<T> *curr = last->next;
  while (curr->next != last) 
  {
    curr = curr->next;
  }

  curr->next = curr->next->next;
  delete last;
  last = curr; 
}
```

We have a list like the below.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e4ef993d-499d-47ea-ae1f-e6586fef779a/cll-singly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=8be6c8258d988e3076cd0521b5da8952e362e90112ce105599f002dc0732a669&X-Amz-SignedHeaders=host)

In order to remove `last`, we need `last->prev`. But we don't have `prev` in a singly list, thus we need to traverse the list from the beginning upto where `last->prev` is, which is B in the figure.

Now when we're at B, we update its link and let it point to the `head`.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/23917573-da28-4d1d-93d3-db5518864907/cll-singly-remove-at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=46c29a889c56a2fa6b6ace4394e3a77a73311ba94b9149add4de00c5cc187556&X-Amz-SignedHeaders=host)

Then we delete our current `last` and we're done.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef639135-e65b-4a37-8901-48d33735834d/cll-singly-remove-at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=365fae84a9348ea19ec560e7ad7710abc5919bf905291081d5a3203a90268376&X-Amz-SignedHeaders=host)

### circular doubly linked list

```cpp
template <class T>
void CircularDoublyLinkedList<T>::remove_back()
{
  Node<T> *temp = head->prev;
  head->prev->prev->next = head;
  head->prev = head->prev->prev;
  delete temp;
}
```

It looks complicated compare to the singly linked list, but it's actually much simpler.

First please take a look at the below and see which refers to which.

-   `head->prev` == `last`
-   `head->prev->prev` == `last->prev`
-   `head->prev->prev->next` == `last->prev->next`

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/89076692-d5a1-43a2-b11a-ade9d350bc96/cll-doubly-remove-at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=e4260f4b0bd775d2fa0cdfccf9fb2a358033d07fb2638099c6aec5e6505b3bec&X-Amz-SignedHeaders=host)

Hopefully it's not that confusing. We need to connect `last->prev->next` with the `head`.

And change `head->prev`'s link from `last` to `last->prev`.

## View full code
- https://github.com/eubug17/ds-algo/tree/master/linkedlist/circular