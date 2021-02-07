tags: #cll #linkedlist #data-structure #japanese 

<hr />

[[200718 What is a Circular Linked List | 🇺🇲 English]]
[[200718 원형 연결 리스트(Circular Linked List)란 | 🇰🇷 한국어]]

## 循環リストとは？

**単方向**と**双方向連結リスト**では `nil`を指しているノードを探すごとによってリストの最後を見つけることができます。双方向リストの場合には`prev`もあるので`nil`を指しているノードが基本的に二つです。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7c3a7a09-5151-4ca1-9920-fa54d7af6190/cll-doubly-example.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=a712ad3436c81e74219e9215b856d576318df8fe63a394ccc515b9a6b6436262&X-Amz-SignedHeaders=host)

その反面、循環リストとには`nil`がないです。つまり、終わりがないリストです。最後のノードの`next`は最初のノード指すようになっています。双方向リストの場合最初のノードの`prev`は最後のノードに戻ります。このため**循環**リストとよびます。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fe881d2f-26ab-4836-851f-484157291e3a/cll-doubly.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=d1c3dd39524e1960464055c46690e4aaff30e27ce7fe97915dd8286e175e1a0c&X-Amz-SignedHeaders=host)

## ノードの構造

循環リストは単方向と双方向の変形なので、ノードの構造はどのタイプのリストを使うかによって変わります。

### **単方向循環リスト**

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

### **双方向循環リスト**

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

## 実装

今から説明する循環リストとの構造です。全てのコードは該当記事の下のGitHubリンクを参照してください。

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

## コンストラクター

### **単方向循環リスト**

単方向連結リストの場合ほとんどの演算が最初のノードに接近することから始まります。なので普段`head`とか`first`などな名のメンバー変数が定義されています。 しかし、単方向循環リストの場合はすこし違います。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/707a65bc-567f-4a04-a497-c24b4ce2e048/cll-singly-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=305994d70dccc4905054c5c079ac7850a4639d24a2a862701de17824c2d4039d&X-Amz-SignedHeaders=host)

循環という特性を利用して最初ノードではなく最後のノードを保存して実装します。変数の名は`tail`とか`last`が普段使われます。

```cpp
template <class T>
CircularLinkedList<T>::CircularLinkedList(int val)
{
  last = new Node(val);
  last->next = last;
}
```

`last`ノードを使うとすごく便利です。まず`last`と`last->next`でリストの最初と最後、両方すぐ接近することができます。そして、リストの最後にノードを追加することとか、最初のノードを削除することが簡単にできます。

### **双方向循環リスト**

双方向リスト場合`next`と`prev`を使って両方向移動するのができます。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bcfbe732-5e91-42a6-8e3d-08795bff08ed/cll-doubly-insert1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=28721274fe759b4051d987b0e81eb6c1c32322abf45dbad2ee8d9a8dd943effb&X-Amz-SignedHeaders=host)

なので`head`と`last`どちを使ってもファフォマンスの差はないので自由に選んで実装してください.一般的には`head`を定義するのでこの記事でも`head`を使います。

```cpp
template <class T>
DoublyLinkedList<T>::DoublyLinkedList(int val)
{
  head = new Node(val);
  head->next = head->prev = head;
}
```

## 最初にノードを挿入

### **単方向循環リスト**

```cpp
template <class T>
void CircularSinglyLinkedList<T>::insert_front(int val) 
{
  Node<T> *newNode = new Node(val);
  newNode->next = last->next;
  last->next = newNode;
}
```

新しいノード`newNode`をリストの最初のノード（`last->next`）と繋ぎます。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6acda366-905c-4ffa-b11d-dd069eff9731/cll-singly-insert_at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=631e7463099a0eabaec2da62dea4cb1de1b61eacc68ec3d8db84e1dd96063b99&X-Amz-SignedHeaders=host)

上の表を参照してください。現在`last->next`はAと繋がれています。これが`newNode`を指すようにノードのリンクを変えると終わりです。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3a44e82-aeea-4eee-b883-eb11b9a17e45/cll-singly-insert_at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=e3e2ef46850d32a994ea02510f432b5dffe47a4519c26324dc4d71d654a965c0&X-Amz-SignedHeaders=host)

### **双方向循環リスト**

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

まずは新しいノードの`next`と`prev`を`head`と`last`それぞれにつなげます。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/be260084-0a88-456e-84f4-6c4cfe3efb5f/cll-doubly-insert_at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=745d7adca491994926acfd41c2d0c9c7ec0eec663eb096ca407af57774024cff&X-Amz-SignedHeaders=host)

今`last->next`は`head`を指しています。このノードを`newNode`とリンクします。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c83c6e1a-080e-4f9f-ac1d-08212b817ee5/cll-doubly-insert_at4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=16fb6d24e92a47c2cc1d11eeae7912a9189c8c735b254b69d751ab097d111935&X-Amz-SignedHeaders=host)

そして最後に`head->prev`が`last`ではなく`newNode`を指すようにリンクを更新するとおわりです。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f44c4c8-d1e8-4aef-ad81-a759ffddd03d/cll-doubly-insert_at5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=36cbb861dca222d25fe9271db968b39fc200a8b80e06985d2296dab7dbab9aad&X-Amz-SignedHeaders=host)

## 最後にノードを挿入

### **単方向循環リスト**

この記事の最初に、`tail`ノードを使うとリストの最後に新しいノードを挿入することが簡単になると説明しました。

本当に簡単になるか下記のコードみてください。まずは`tail`がなかった場合のコードです。

```cpp
template <class T>
void CircularSinglyLinkedList<T>::insert_back(int val) 
{
  Node<T> *temp = head;

  while (temp->next != nullptr) 
  {
    temp = temp->next;
  }

  Node<T> *newNode = new Node(val);
  temp->next = newNode;
}
```

リストの最初から順番に最後まで進んで、そこから新しいノードを挿入しています。 この演算の時間複雑度はO(N)になります。

では`last`を使うと、どうなるかみてみましょう。

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

まずは`newNode->next`がリストの最初を指しようにします。最初のノードは`last->next`で接近できます。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ed7152f6-bbf6-492c-83e9-57f5a07f0a2e/cll-singly-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=ab12e861c0bc13f2e7760c48586c5287d4fb8c7da851ee4ab0e3c9748b099801&X-Amz-SignedHeaders=host)

その後`last->next`を`newNode`と繋ぎて、`last`を`newNode`に変えることだけで終わりです。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f5d38300-468b-457b-857b-f3c467ee9efb/cll-singly-insert3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=8f753092b95037876b12b9794e45c1bace6060aa2f10d4f884fdc2944851359c&X-Amz-SignedHeaders=host)

`last`を使うとリストの最後にノードを挿入することがO(1)時間にできます。

### **双方向循環リスト**

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

`newNode->prev`と`newNode->next`を今の`last`と`head`にそれぞれ繋ぎます。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dbae4da0-b1ab-493e-8483-ab0fc7b79b5f/cll-doubly-insert2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=1d322032a0a5722c7cd31cc339c7f36bc5eea6c31b0ff919c3a1f25c7e5b3dd6&X-Amz-SignedHeaders=host)

今の`last`、つまり**B**、は`head`を指しています。これは`newNode`を指しようにリンク変えます。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c05c3d51-4b43-4dee-a6f6-f89f85224c14/cll-doubly-insert3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=075d02782fe0745c43d8a4de923946f38cd6ef22ab4e8b5800993f8af8206189&X-Amz-SignedHeaders=host)

最後に`head->prev`を`newNode`と繋ぐと終わりです。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b2f1c9a-769f-41fd-8457-32f2b9a71bb5/cll-doubly-insert4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=1ca4cf0498d1eac18afe4dcb5a10eda39fe1ede4da46e37321f207305fdf8a39&X-Amz-SignedHeaders=host)

## 最初のノードの削除

### **単方向循環リスト**

```cpp
template <class T>
void CircularSinglyLinkedList<T>::remove_front()
{
  Node<T> *temp = last->next;
  last->next = last->next->next;

  delete temp;
}
```

`last`ノードがあるため、最初のノードを削除する手順は簡単です。

下記のようにリストがあるとしましょう。このリストには三つの要素があります。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2a61b93d-0230-4c6c-9e26-acc583d92467/cll-singly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=6d241f1c322643ae169cc80dfcc8f15eed75697e0369f5ea75a8cd0af435cd0c&X-Amz-SignedHeaders=host)

`last->next`は`head`を指していますが、これを`last->next->next`とリンクすることだけで終わりです。 そして`last->next`は`delete`します。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9e7558f7-6888-4712-aca3-c512281866ac/cll-doubly-remove-at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=228579d333485e553e1c0b6d3e1f841da04fb6c0c4f5fa8a7cc12131065e71b2&X-Amz-SignedHeaders=host)

### **双方向循環リスト**

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

双方向循環リストの場合も簡単です。もしかしたら単方向リストより簡単かもしれません。

下記のようなリストが与えられたと想定してとき、`head`を削除してみましょ。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2c497d36-9238-4097-b2c3-f392188b5dd3/cll-doubly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=c6091e9bf8b3afb866f9657e1430152479d67de0dce5dacf39e289247725db90&X-Amz-SignedHeaders=host)

`head`とつながっている全てのノードを外します。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a92b0e2f-8b95-4014-9e85-86b3c8e66a97/cll-doubly-remove-at1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=dbba6f106a44f8d03359ba6604187ef0a94b8b95e8bd4c000c88883fdbb96a3c&X-Amz-SignedHeaders=host)

そして`head`を更新すれば終わりです。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/183d9e0e-8552-449f-b153-c840def10f2a/cll-doubly-remove-at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=3caca4f5e321aa35a9c586f9f0913a8fbf129ccae4a8ce3b9e5ca8ef7167f017&X-Amz-SignedHeaders=host)

## 最後のノードの削除

### **単方向循環リスト**

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

以下のようなリストがあります。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e4ef993d-499d-47ea-ae1f-e6586fef779a/cll-singly-remove-at0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=8be6c8258d988e3076cd0521b5da8952e362e90112ce105599f002dc0732a669&X-Amz-SignedHeaders=host)

最後のノード`last`を削除するためには`last->prev`が必要ですが、単方向リストには`prev`がありません。 なのでリストの最初から順番に進んでラストの前(**Bノード**)を接近しなければなりません。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/23917573-da28-4d1d-93d3-db5518864907/cll-singly-remove-at2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=46c29a889c56a2fa6b6ace4394e3a77a73311ba94b9149add4de00c5cc187556&X-Amz-SignedHeaders=host)

**B**ノードまで到達したら、該当ノードの`next`が`last`ではなく`head`を指すように変えます。 そして`last`を更新すると終わりです。

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef639135-e65b-4a37-8901-48d33735834d/cll-singly-remove-at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=365fae84a9348ea19ec560e7ad7710abc5919bf905291081d5a3203a90268376&X-Amz-SignedHeaders=host)

### **双方向循環リスト**

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

単方向リストと比べると複雑そうに見えますが、実は`prev`があるので簡単に実装できます。

「head->prev->prev->nextってなに？」と思う方がいると思うので下記のリストをみてください。 左側のノードが意味するのが右と同じです。

-   `head->prev` == `last`
-   `head->prev->prev` == `last->prev`
-   `head->prev->prev->next` == `last->prev->next`

![cll](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/89076692-d5a1-43a2-b11a-ade9d350bc96/cll-doubly-remove-at3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210207%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210207T044544Z&X-Amz-Expires=86400&X-Amz-Signature=e4260f4b0bd775d2fa0cdfccf9fb2a358033d07fb2638099c6aec5e6505b3bec&X-Amz-SignedHeaders=host)

`head->prev->prev->next`が`head`を指すようにリンクを変えます。そして`head->prev`を`last`から`last->prev`を指すようにすると終わりです。

## 全体コード
- https://github.com/eubug17/ds-algo/tree/master/linkedlist/circular
