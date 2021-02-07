tags: #sll #linkedlist #data-structure #korean 

<hr />

[[200510 What is a Singly Linked List | 🇺🇲 English]]
[[200510 単方向リスト(Singly Linked List)とは | 🇯🇵 日本語]]

## 단일 연결 리스트란?

단일 연결 리스트는 한방향으로만 노드들이 연결되어 있는 리스트이며, 각 노드는 메모리 어딘가에 있는 노드를 참조 할 `next` 포인터를 지니고 있습니다.

![linked list](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/13fc5017-66a7-480f-8edc-bc7d598f5410/linkedlist.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052835Z&X-Amz-Expires=86400&X-Amz-Signature=a2fe925fe0d86fb7a41fde368e03dcde23fcf9c293954ca648950501b14a9343&X-Amz-SignedHeaders=host)

각 노드는 아래의 정보를 지니고 있습니다:

1.  다음 노드를 참조 할 `next` 포인터.
2.  데이터 값을 저장하는 `data` 변수.

```cpp
template <class T>
class Node 
{
  private:
  public:
    Node(T data) : next(nullptr) { this->data = data; }

    Node<T> *next;
    T data;
};
```

## 구현

아래는 구현 해당 포스트에서 구현 할 단일 연결 리스트의 구조입니다.

```cpp
template <class T>
class SinglyLinkedList
{
  private: 
    Node<T> *head;
    Node<T> *tail;
    int size;

  public:
    SinglyLinkedList();
    SinglyLinkedList(T data);
    ~SinglyLinkedList();

    void push_front(T data);
    void push_back(T data);
    void push_at(int index, T data);

    void pop_front();
    void pop_back();
    void pop_at(int index);

    T peek_first();
    T peek_last();

    void traverse();

};
```

`tail`은 리스트의 마지막 노드를 가리킵니다. `tail`을 사용하면 리스트 끝에 노드를 삽입할시, 불필요하게 머리부터 끝까지 순회 할 필요가 없어집니다.

단인 연결 리스트의 함수들을 살펴보도록 합시다.

## 생성자

디폴트와 첫 노드의 값을 인자로 하나 받는 매개변수 생성자, 이렇게 두 개를 정의했습니다.

### 디폴트 생성자

멤버 변수들을 기본값으로 초기화 해줍니다.

```cpp
/* 기본 생성자 */
template <class T>
SinglyLinkedList<T>::SinglyLinkedList()
{
  head = tail = nullptr;
  size = 0;
}
```

### 매개변수 생성자

파라미터로 받은 값을 기반으로 노드를 생성, `head`와 `tail`이 해당 노드를 가리키게 됩니다.

![### parameterized constructor](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/71073f3c-e422-43e2-82f0-bbc3e52e0bb5/sll-constructor-1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052835Z&X-Amz-Expires=86400&X-Amz-Signature=1ae45f07d61788b9c32dedf9b094b0d7d5f5a4441a1d092a030b58ba1ba1cf69&X-Amz-SignedHeaders=host)

```cpp
/* 매개변수 생성자 */
template <class T>
SinglyLinkedList<T>::SinglyLinkedList(T data)
{
  head = new Node(data);
  tail = head;
  size = 1;
}
```

## 데이터 추가하기

새로운 노드는 리스트의 처음, 중간, 그리고 끝에 삽입이 가능합니다.

### 리스트 처음에 노드 삽입하기

1.  새로운 노드 `newNode` 생성.
2.  `newNode`가 현재의 머리를 가리키도록 한다.
3.  `head`를 업데이트 한다.
4.  (`tail`노드를 사용하는 경우 `tail`도 업데이트 한다.)

```cpp
template <class T>
void SinglyLinkedList<T>::push_front(T data) 
{
  Node<T> *temp = new Node<T>(data);
  temp->next = head;
  head = temp;

  if (tail == nullptr)
  {
    tail = head;
    tail->next = nullptr;
  }

  ++size;
}
```

### 리스트 끝에 노드 추가하기

1.  새로운 노드 `newNode` 생성
2.  `tail->next`가 `newNode`를 가리키도록 한다.
3.  `newNode`가 `tail`이 되도록 `tail`을 업데이트 한다.

`tail`을 사용하지 않을 경우, 리스트를 순회해서 마지막 노드 까지 하나하나 방문해야 하는 불필요한 작업을 거쳐야 합니다.

```cpp
template <class T>
void SinglyLinkedList<T>::push_back(T data) 
{
  Node<T> *temp = new Node<T>(data);
  tail->next = temp;
  tail = temp;
  tail->next = nullptr;

  ++size;
}
```

### 리스트 중간에 노드 추가하기

매개변수로 넘어온 `index` 위치에 노드를 삽입하려고 하는 과정입니다.

1.  `index-1`번 째 노드를 찾고 이를 `temp`노드에 저장.
2.  새로운 노드 `newNode`를 생성.
3.  `temp`와 `temp->next`사이에 `newNode`를 삽입한다. 위에서 설명한 리스트 처음에 노드를 삽입하는 과정과 같다. 다만 `head`대신 `temp`를 사용.

```cpp
template <class T>
void SinglyLinkedList<T>::push_at(int index, T data)
{
  Node<T> *temp = head;
  for (int i=0; i<index-1; ++i)
  {
    temp = temp->next;
  }

  Node<T> *newNode = new Node<T>(data);
  newNode->next = temp->next;
  temp->next = newNode;
  ++size;
}
```

## 데이터 삭제하기

### 첫 번째 노드 삭제하기

첫 번째 노드를 삭제하는 방법은 생각보다 되게 간단합니다.

1.  우선 `head`를 임시 포인터에 저장. 그리고
2.  `head`를 `head->next`로 업데이트.
3.  임시 포인터에 저장해놓은 이전 `head` 포인터의 메모리를 해제해준다 (노드를 지운다).

```cpp
template <class T>
void SinglyLinkedList<T>::pop_front()
{
  Node<T> *temp = head;
  head = head->next;
  delete temp;
}
```

### 마지막 노드 삭제하기

1.  마지막 노드의 이전 노드에 접근.
2.  마지막 노드의 메모리 할당을 해제한다 (노드를 지운다).
3.  `tail`을 사용하는 경우, `tail`의 포인터를 업데이트 한다.

```cpp
template <class T>
void SinglyLinkedList<T>::pop_back()
{
  if (size == 1)
  {
    delete head;
    head = tail = nullptr;
    size = 0;
    return;
  }

  Node<T> *temp = head;
  for (int i=1; i<size-1; ++i)
  {
    temp = temp->next;
  }

  delete temp->next;
  temp->next = nullptr;
  tail = temp;
}
```

### 중간 노드 삭제하기

바로 위에서 설명 한 마지막 노드 삭제하기와 작동방법은 동일합니다. 다만 위에서는 마지막 노드의 이전 노드까지 이동했다면, 여기서는 마지막 노드가 아닌 `index`의 이전, 즉 `index-1`까지 이동해줍니다. 그 후는 위에서 언급한 동작방법과 동일합니다.

```cpp
template <class T>
void SinglyLinkedList<T>::pop_at(int index)
{
  Node<T> *temp = head;
  for (int i=0; i<index-1; ++i)
  {
    temp = temp->next;
  }

  Node<T> *temp2 = temp->next;
  temp->next = temp->next->next;
  delete temp2;
}
```

## 연결리스트 순회

단일 연결리스트를 순회하는 방법입니다. 머리(`head`)부터 접근해서 그 다음 노드가 꼬리일때까지 반복합니다.

```cpp
template <class T>
void SinglyLinkedList<T>::traverse()
{
  Node<T> *temp = head;
  while(temp->next != nullptr) 
  {
    cout << temp->data << ' ';
    temp = temp->next;
  }

  cout << temp->data << endl;
}
```

## 전체 코드 보기
- https://github.com/eubug17/ds-algo/blob/master/linkedlist/singly/sll.hpp