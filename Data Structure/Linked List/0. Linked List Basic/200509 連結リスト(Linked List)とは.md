tags: #linkedlist #data-structure #japanese

<hr />

[[200509 What is a Linked List | 🇺🇲 English]]
[[200509 연결 리스트(Linked List)란 | 🇰🇷 한국어]]

## 連結リストとは

連結リスト（リンクドリスト；英. Linked List）はオブジェクトを線形順序に保存するデータ構造です。この順序ですが、配列と同じようにインデックスではなく、それぞれのオブジェクトのポインターで決められます。

![linkedlist](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/637ddad6-f0c7-47df-b785-fd6591e7b74f/linkedlist.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052834Z&X-Amz-Expires=86400&X-Amz-Signature=24d1f33e76b81324d99db19542d74bdcd6312d21280e0aca41782f1c2e382370&X-Amz-SignedHeaders=host)

## node

リストのそれぞれのオブジェクトを<b>ノード（node）</b>とよびます。

ノードはdataと他のノードを示すポインターで構成されています。この他のノードというのは、例えば次のノード（`next`）とか前のノード（`prev`）があります。

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


| 連結リストのタイプ | 説明 |
|-----------------|--------------|
| 単方向リスト（Singly Linked List) |  順番につながっているので片方にだけ移動ができる連結リスト |
| 双方向リスト（Doubly Linked List） | ノードが両方向でつながっている連結リスト |
| 循環リスト（Circular Linked List）|最後のノードのnextは最初を、最初のノードのprevは最後を指す。 |
| 整列リスト （Sorted List）| 単方向、双方向、または循環リストの全てノードがdataの値で整列されているリスト |

## operations

### search(L, k)

list `L`の中からkey `k`が含まれる最初の要素を探します。

```cpp
Node* search(Node *L, int key) 
{
  Node *curr = L->head;
  while (curr->next != nullptr and curr->key != key)
    curr = curr->next;

  return curr;
}
```

時間複雑度：O(n)

### insert(L, x)

リストLの最初に要素xを挿入します。

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

時間複雑度：O(1)

### delete(L, x)

リスト`L`の中から要素`x`を削除します。

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

時間複雑度：O(1)

## sentinels

Sentinelノードを使うことでinsertとdelete関数の中のheadとtailの境界条件を適応させないことができます。Sentinelはheadとtailの 間に書かれているので、ダミーノードであり、値とされないません。

`sentinel->next`はリストの最初（head）を示し、`sentinel->prev`はリストの最後（tail）を示します。

![sentinels](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9c60e716-0d80-44d6-82f4-1f1d84920375/sentinel-node.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210206%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210206T052834Z&X-Amz-Expires=86400&X-Amz-Signature=3f307c77d869a672831f10a84dcfe1ba541f332205699eb66d328242e26ce9fa&X-Amz-SignedHeaders=host) 
img src: Introduction to Algorithms, 3rd Edition (CLRS)

**(a)** → 空リストであり、sentinelだけが入っています。

**(b)** → `sentinel->next`がリストの最初を、そして`sentinel->prev`がリストの最後を示しています。

以上をもとに`insert`と`delete`関数を下記のように簡略化することができます。

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

sentinelはパフォマンスに影響をあたえないので慎重に使用しなければいけません。特に多くの短いリストを使う場合、余分なノード（`sentinel node`）を加えることでメモリーに負担をかけることがあります。

なのでsentinelはコードの簡略化が確実にできる場合のみ使います。

## 連結リストの長所

-   連結リストは[動的](http://e-words.jp/w/%E5%8B%95%E7%9A%84.html)です。
-   挿入・削除の演算時間が配列より早いです。

## 連結リストの短所

-   リストにある要素にアクセスしたい場合、初めから順番に進まなければいけない。
-   新しいデータは新しいノードを意味するので、メモリの使用量が増えます。
-   参照の局所性（locality of reference）がないので[キャッシュフレンドリー](https://qastack.jp/programming/16699247/what-is-a-cache-friendly-code)ではない。

時間複雑度

| 演算 | 配列 | 連結リスト |
|------|------|-----------|
|  接近 |  O(1) | O(n) |
| 探索 | O(n) | O(n) |
| 挿入 | O(n) | O(1) |
| 削除 | O(n) | O(1) |

## Reference
-   Introduction to Algorithms, 3rd Edition (CLRS)