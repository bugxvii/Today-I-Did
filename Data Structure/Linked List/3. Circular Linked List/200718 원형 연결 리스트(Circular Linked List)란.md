tags: #cll #linkedlist #data-structure #korean

<hr />

[[200718 What is a Circular Linked List | 🇺🇲 English]]
[[200718 循環リスト(Circular Linked List)とは | 🇯🇵 日本語]]

## 원형 연결 리스트란

**단일**과 **이중 연결 리스트**에서는 `nil`을 가리키는 노드를 찾으므로써 리스트의 마지막이 어디인지 확인할 수 있습니다; 이중 연결 리스트의 경우에는 `prev`도 있기 때문에 아래의 그림 처럼 두 개의 노드가 `nil`을 가리키죠.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7c3a7a09-5151-4ca1-9920-fa54d7af6190/cll-doubly-example.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=a712ad3436c81e74219e9215b856d576318df8fe63a394ccc515b9a6b6436262&X-Amz-SignedHeaders=host)

그 반면 원형 연결 리스트에는 `nil`이 없습니다. 즉, 끝이 존재하지 않죠. 마지막 노드는 `nil`이 아닌 첫 번째 노드를 가리키고, `prev`가 있는 원형 이중 리스트의 경우 첫 번째 노드의 `prev` 역시 `nil`이 아닌 마지막 노드를 가리킵니다. 그렇기 때문에 이름 그대로 _원형_, 돌고 도는 구조입니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fe881d2f-26ab-4836-851f-484157291e3a/cll-doubly.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=d1c3dd39524e1960464055c46690e4aaff30e27ce7fe97915dd8286e175e1a0c&X-Amz-SignedHeaders=host)

## 노드의 구조

원형 리스트는 단일과 이중 리스트의 변형이기 때문에 어떤 리스트를 기반으로 하느냐에 따라 노드의 구조가 달라집니다.

### **원형 단일 리스트**

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

### **원형 이중 리스트**

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

## 구현

여기서 구현 할 원형 연결 리스트의 기본 구조입니다. 

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

## 생성자

### **원형 단일 리스트**

단일 리스트의 경우 대부분의 연산들이 리스트의 첫 번째 노드에 접근하는 것으로부터 시작됩니다. 그래서 보통 `head` 또는 `first` 등의 이름의 멤버 변수가 정의되어 있죠.

하지만 원형 단일 리스트의 경우는 조금 다릅니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/707a65bc-567f-4a04-a497-c24b4ce2e048/cll-singly-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=305994d70dccc4905054c5c079ac7850a4639d24a2a862701de17824c2d4039d&X-Amz-SignedHeaders=host)

돌고 도는 구조의 특성을 이용해서 첫 번째 노드가 아닌 마지막 노드를 저장해서 사용합니다. 이름은 `tail` 또는 `last`가 주로 사용되는데 여기서는 `last`를 사용했습니다.

```cpp
template <class T>
CircularLinkedList<T>::CircularLinkedList(int val)
{
  last = new Node(val);
  last->next = last;
  size = 1;
}
```

`last` 노드를 사용하는데에 대한 이점은 분명히 존재합니다. 우선 `last`와 `last->next`로 리스트의 처음과 마지막에 바로 접근이 가능합니다. 또한, 리스트의 마지막에 새로운 노드를 추가하거나 첫 번째 리스트를 삭제 할 때, 리스트 전체를 순회 할 필요없이 O(1)시간에 바로 삽입과 제거가 가능합니다.

### **원형 이중 리스트**

이중 리스트의 경우 `next`와 `prev` 포인터를 이용해서 양방향으로 이동이 가능합니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bcfbe732-5e91-42a6-8e3d-08795bff08ed/cll-doubly-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=28721274fe759b4051d987b0e81eb6c1c32322abf45dbad2ee8d9a8dd943effb&X-Amz-SignedHeaders=host)

때문에 `head`를 정의하던 `last`를 정의하던 다를게 없기 때문에 편하신대로 구현하시면 됩니다. 일반적으로는 `head`를 정의하기 때문에 저도 `head`를 사용했습니다.

```cpp
template <class T>
DoublyLinkedList<T>::DoublyLinkedList(int val)
{
  head = new Node(val);
  head->next = head->prev = head;
  size = 1;
}
```

## 리스트 머리에 데이터 추가

### **원형 단일 리스트**

```cpp
template <class T>
void CircularSinglyLinkedList<T>::insert_front(int val) 
{
  Node<T> *newNode = new Node(val);
  newNode->next = last->next;
  last->next = newNode;
}
```

새로운 노드인 `newNode`가 리스트의 첫 노드인 `last->next`를 가리키도록 합니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6acda366-905c-4ffa-b11d-dd069eff9731/cll-singly-insert_at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=631e7463099a0eabaec2da62dea4cb1de1b61eacc68ec3d8db84e1dd96063b99&X-Amz-SignedHeaders=host)

위의 그림을 보면 현재 `last->next`는 A와 연결되어 있습니다 . 새로운 노드를 머리에 추가했기 때문에 `last->next`가 `newNode`와 연결되도록 링크를 업데이트 해주면 됩니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3a44e82-aeea-4eee-b883-eb11b9a17e45/cll-singly-insert_at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=e3e2ef46850d32a994ea02510f432b5dffe47a4519c26324dc4d71d654a965c0&X-Amz-SignedHeaders=host)

### **원형 이중 리스트**

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

먼저 새로운 노드의 `next`와 `prev`부터 연결해줍니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/be260084-0a88-456e-84f4-6c4cfe3efb5f/cll-doubly-insert_at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=745d7adca491994926acfd41c2d0c9c7ec0eec663eb096ca407af57774024cff&X-Amz-SignedHeaders=host)

현재 `last->next`는 `head`를 가리키고 있죠. `last->next`를 `newNode`와 연결합니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c83c6e1a-080e-4f9f-ac1d-08212b817ee5/cll-doubly-insert_at4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=16fb6d24e92a47c2cc1d11eeae7912a9189c8c735b254b69d751ab097d111935&X-Amz-SignedHeaders=host)

그리고 마지막으로 `head->prev`가 `last`로 되돌아 가는 것이 아닌, `newNode`를 가리키도록 링크를 업데이트 합니다. 그리고 `head`를 `newNode`로 바꿔주면 됩니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f44c4c8-d1e8-4aef-ad81-a759ffddd03d/cll-doubly-insert_at5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=36cbb861dca222d25fe9271db968b39fc200a8b80e06985d2296dab7dbab9aad&X-Amz-SignedHeaders=host)

## 리스트 끝에 데이터 추가

### **원형 단일 리스트**

생성자 부분에서 잠깐 설명했습니다만, 단일 리스트에서 `last`를 사용하면 리스트 끝에 데이터를 삽입하는 과정이 상당히 간단해집니다. 아래의 코드를 확인해보죠.

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

우선 `newNode`의 `next`를 리스트의 첫 번째 노드와 연결해줍니다. 첫 번째 노드는 `last->next`가 가리키고 있죠.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ed7152f6-bbf6-492c-83e9-57f5a07f0a2e/cll-singly-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=ab12e861c0bc13f2e7760c48586c5287d4fb8c7da851ee4ab0e3c9748b099801&X-Amz-SignedHeaders=host)

그 다음, `last->next`를 `newNode`와 연결해주고, `last`를 `newNode`로 바꿔주면 끝입니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f5d38300-468b-457b-857b-f3c467ee9efb/cll-singly-insert3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=8f753092b95037876b12b9794e45c1bace6060aa2f10d4f884fdc2944851359c&X-Amz-SignedHeaders=host)

### **원형 이중 리스트**

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

여기도 마찬가지로 새로운 노드인 `newNode`의 `prev`와 `next`부터 `head`와 `last`에 연결해줍니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dbae4da0-b1ab-493e-8483-ab0fc7b79b5f/cll-doubly-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=1d322032a0a5722c7cd31cc339c7f36bc5eea6c31b0ff919c3a1f25c7e5b3dd6&X-Amz-SignedHeaders=host)

위 그림에서 B에 해당하는 리스트의 `last`가 `head`와 연결되어 있습니다. 이 링크를 업데이트해서 `newNode`와 연결합니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c05c3d51-4b43-4dee-a6f6-f89f85224c14/cll-doubly-insert3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=075d02782fe0745c43d8a4de923946f38cd6ef22ab4e8b5800993f8af8206189&X-Amz-SignedHeaders=host)

마지막으로 `head`의 `prev`를 B가 아닌 `newNode`와 연결되도록 업데이트 하면 모든 노드가 잘 이어져 있는것을 확인할 수 있습니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b2f1c9a-769f-41fd-8457-32f2b9a71bb5/cll-doubly-insert4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=1ca4cf0498d1eac18afe4dcb5a10eda39fe1ede4da46e37321f207305fdf8a39&X-Amz-SignedHeaders=host)

## 머리 노드 삭제

### **원형 단일 리스트**

```cpp
template <class T>
void CircularSinglyLinkedList<T>::remove_front()
{
  Node<T> *temp = last->next;
  last->next = last->next->next;

  delete temp;
}
```

`last` 노드가 있기 때문에 첫 번째 노드의 삭제는 간단히 가능합니다.

아래와 같이 세 개의 노드가 있다고 생각해봅시다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2a61b93d-0230-4c6c-9e26-acc583d92467/cll-singly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=6d241f1c322643ae169cc80dfcc8f15eed75697e0369f5ea75a8cd0af435cd0c&X-Amz-SignedHeaders=host)

`last->next`가 `head`를 가리키고 있는데 이를 `last->next->next`와 연결해주면 끝입니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9e7558f7-6888-4712-aca3-c512281866ac/cll-doubly-remove-at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=228579d333485e553e1c0b6d3e1f841da04fb6c0c4f5fa8a7cc12131065e71b2&X-Amz-SignedHeaders=host)

### **원형 이중 리스트**

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

원형 이중 리스트의 경우도 생각보다 간단합니다.

다시 한 번 아래와 같이 세 개의 노드가 앞뒤 이중으로 연결되어 있다고 생각해 봅시다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2c497d36-9238-4097-b2c3-f392188b5dd3/cll-doubly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=c6091e9bf8b3afb866f9657e1430152479d67de0dce5dacf39e289247725db90&X-Amz-SignedHeaders=host)

먼저 `head`와 연결되어 있는 모든 링크들을 끊어줍니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a92b0e2f-8b95-4014-9e85-86b3c8e66a97/cll-doubly-remove-at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=dbba6f106a44f8d03359ba6604187ef0a94b8b95e8bd4c000c88883fdbb96a3c&X-Amz-SignedHeaders=host)

그리고 `head`는 바로 삭제해주면 되기 때문에 굳이 `head`에서 연결된 링크들을 건들 필요는 없습니다. 간단하죠?

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/183d9e0e-8552-449f-b153-c840def10f2a/cll-doubly-remove-at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=3caca4f5e321aa35a9c586f9f0913a8fbf129ccae4a8ce3b9e5ca8ef7167f017&X-Amz-SignedHeaders=host)

## 마지막 노드 삭제

### **원형 단일 리스트**

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

아래와 같은 리스트가 있습니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e4ef993d-499d-47ea-ae1f-e6586fef779a/cll-singly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=8be6c8258d988e3076cd0521b5da8952e362e90112ce105599f002dc0732a669&X-Amz-SignedHeaders=host)

마지막 노드인 `last`를 삭제하기 위해서는 `last->prev`가 필요하지만 단일 리스트에 `prev`는 없죠. 그렇기 때문에 직접 머리부터 시작해서

`last`이전 노드까지 이동해줍니다. 위 그림에서는 B에 해당하는 부분이죠.

B에 도달했으면 해당 노드의 `next`를 다음다음 (`next->next`)와 연결합니다. 쉽게말해 `head`(A)와 연결해주면 됩니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/23917573-da28-4d1d-93d3-db5518864907/cll-singly-remove-at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=46c29a889c56a2fa6b6ace4394e3a77a73311ba94b9149add4de00c5cc187556&X-Amz-SignedHeaders=host)

`last`를 삭제하고 `last`를 B로 바꿔주면 됩니다.

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef639135-e65b-4a37-8901-48d33735834d/cll-singly-remove-at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=365fae84a9348ea19ec560e7ad7710abc5919bf905291081d5a3203a90268376&X-Amz-SignedHeaders=host)

### **원형 이중 리스트**

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

얼핏보면 복잡해 보이지만 `prev` 포인터가 있기때문에 단일 리스트보다 훨씬 간단합니다.

헷갈릴수도 있으니 일단 간략히 아래의 표를 확인해주세요.

-   `head->prev` == `last`
-   `head->prev->prev` == `last->prev`
-   `head->prev->prev->next` == `last->prev->next`

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/89076692-d5a1-43a2-b11a-ade9d350bc96/cll-doubly-remove-at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=e4260f4b0bd775d2fa0cdfccf9fb2a358033d07fb2638099c6aec5e6505b3bec&X-Amz-SignedHeaders=host)

이를 이용해서 `last->prev->next`가 `head`와 연결되도록 업데이트 합니다. 마찬가지로 `head->prev`를 `last`에서 `last->prev`로 업데이트 해주면 끝입니다.

## 전체 코드 보기
- https://github.com/eubug17/ds-algo/tree/master/linkedlist/circular