tags: #dll #linkedlist #data-structure #japanese 

<hr />

[[200711 What is a Doubly Linked List | 🇺🇲 English]]
[[200711 이중 연결 리스트(Doubly Linked List)란 | 🇰🇷 한국어]]

## 双方向連結リストとは?

双方向連結リストはー方向にだけ移動することができた単方向リストとは違い、両方向に移動することができるデータ構造です。双方向リストのそれぞれのノードは`prev`と`next`二つのポインターを持っています。`prev`は現在ノードの以前、`next`は次のノードを指すようになります。

例えば下記のようなリストがあるとき、２番目のノード（**B**）の前の次のノードは`B-prev`と`B->next`で接近できます。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3484b447-1446-4b29-8bae-9e7db88a9a49/dll.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=6830acbd11940d8f751c0fde906b69187bd64e3365acd553aeb83f3cbc0b52d9&X-Amz-SignedHeaders=host)

## ノードの構造

上に述べたとおり双方向連結リストのそれぞれのノードには二つのノード（`prev`と`next`）が存在します。

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

## 実装

この記事で実装する双方向連結リストの基本構造は下記の通りです。

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

では、それぞれの関数がどういうふうに動作するかみてみましょう。

## コンストラクター

最初ノードのデータ値を媒介変数で受け取って`head`と`tail`ノードを定義します。`tail`はリストの最後のノードを指すために使用されます。

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

## 新しいノードの挿入

`link(curr, newNode)`というhelper関数を実装しました。媒介変数の**１番目の因子**`curr`は現在位置のノードで, **２番目の因子**は`curr`と連結するノードです。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c85274ce-2bb3-4435-9394-b2c8cf14d47e/sll-constructor-1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=bc5960531f62dcc1c808689757a1e579c1b31b68751d651d0a50fe4510c7b239&X-Amz-SignedHeaders=host)

```cpp
template <class T>
void DoublyLinkedList<T>::link(Node<T> *curr, Node<T> *newNode)
{
  curr->next = newNode;
  newNode->prev = curr;
}
```

### リスト最後にノードを挿入

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

まずはリストに存在するノードが`head`だけかを確認します。もしそうなら`link(head, newNode)`を呼び出して`head`と`newNode`を連結します。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c32ce2f9-a64a-4006-be10-1f3c4886db82/dll-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=0d200517f12c1551a35b63ba4160d711f274d0e452b3830cbee2965b06ee40a2&X-Amz-SignedHeaders=host)

リストに一つ以上の要素が存在する場合、`link(tail, newNode)`を呼び出してリストの最後に新しいノードを挿入します。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5bdb3025-2546-4f0a-bc4b-026f007ffb5b/dll-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=39f81cb2fdb21d36d9867978253f5b1704d0f23348497a2108b133e32c0139b9&X-Amz-SignedHeaders=host)

そして`tail`が最後のノードを指すように変えれば完了です。

### リスト最初にノードを追加

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

リスト最後にノードを追加する`insert_back`関数と全く同じです。ただ新しいノードを`tail`ではなく`head`と連結します。

### リストの中間にノードを追加

媒介変数でノードを挿入する位置`index`とノードのデータ値`val`を受け取ります。ちなみに`index`はzero-basedなので0から始めます。

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

無効な`index`を媒介変数から受け取った場合、`insert_front`と`insert_back`を呼び出す方法で対応しました。例えば`index`が負数の場合リストの最初にノードを挿入して、範囲を超過した場合はリストの最後にノードを挿入します。

中間にノードを挿入するときは、挿入する位置にあるノードまで移動しなければいけません。

```cpp
  Node<T> *temp = head;
  for (int i=0; i<index; ++i) 
  {
    temp = temp->next;
  }
```

例えば`index = 1`の場合、下記の表の中で２番目のノード**B**まで移動します。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef15c6aa-59b1-426a-a2ac-07329daae763/dll-insert_at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=c8e0326275fb5807d9762ec6e55828d22ae3e7ecb8cbea67cfa6cde08a29abe2&X-Amz-SignedHeaders=host)

そして新しいノード`newNode`を今の位置そ指してる`temp`の前にあるノード**head**と繋ぎます。

```cpp
  temp->prev->next = newNode;
  newNode->prev = temp->prev;
```

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/65987769-29ab-4e64-84f2-9ff30ce24c07/dll-insert_at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=76d5d3d35cfab176e3b73d463e73421ef57bb5134d8506bc1458d8edeee13f81&X-Amz-SignedHeaders=host)

その後`newNode`と現在挿入する位置にある`temp`をお互いに繋ぐと`index`の位置に`newNode`が挿入されます.

```cpp
  link(newNode, temp);
```

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2decd4ea-098e-4aa3-b50e-e14f54964dcf/dll-insert_at4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=b9e6b0772b22755cfe10c2bce0130dd42317f889c8f0a3d089b4b0d38f3efb86&X-Amz-SignedHeaders=host)

## ノードの削除

### 最後のノードの削除

```
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

下記のようなリストがあるとして、最後のノードをどうやって削除すればいいんですかね。思うより簡単です。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/535954ee-8558-4dd8-be3f-b570019458fd/dll-remove1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=a09b52465a9be94cf979ab8833d841a18d32dd131c66506a1afb384051c407ef&X-Amz-SignedHeaders=host)

まずは`tail`を他の臨時変数に保存します。できたら`tail`を`tail->prev`に移動します。そして臨時に保存したノードをメモリから消します(deallocateする)。 そうしたら終わりです。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3123385-7579-4f38-a2e1-3b21a3a25f06/dll-remove2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=96b13d12df034d79d35581bf4af306bc927e9a096bb0532fce0f42c539f29e80&X-Amz-SignedHeaders=host)

### 最初のノードの削除

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

`tail`ではなく`head`を使用することだけいがいは上から説明した'最後のノードを削除'の動作と全く同じなので、とくに説明はしません。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ebebbf76-ce03-40a9-a4d8-27c1209233a2/dll-remove3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=f0b8e232b15f74af442509c1a379adb0b028946f2fb9d12d593f1ca0b744e242&X-Amz-SignedHeaders=host)

### 中間ノードの削除

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

また以下のような双方向リストがあると想定しましょう。この中で緑のノードを削除します。

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/27d53126-e94a-4b90-8b4e-e30386f6a6d4/dll-remove1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=68e104cb809c53254b51cf27626c6dc38a7ea53e08bab43d9b663648fed66f36&X-Amz-SignedHeaders=host)

まずは削除するノード（緑のノード）がある位置まで移動します。

```cpp
  Node<T> *temp = head;
  for(int i=0; i<index; ++i) 
  {
    temp = temp->next;
  }
```

緑のノードと繋がってる全てのノードを外したあと、緑ノードのメモリをdeallocateすれば完了です。

```cpp
  temp->prev->next = temp->next;
  temp->next->prev = temp->prev;
  delete temp;
```

![dll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9fecf7ac-9e05-4d9c-b960-39f7daf1f39f/dll-remove_at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=b25d13b7b02ccf25d45690122090d5930f941d24daef0b96b3e1eb357c6668d3&X-Amz-SignedHeaders=host)

## 全体コード
- https://github.com/eubug17/ds-algo/blob/master/linkedlist/doubly/dll.hpp