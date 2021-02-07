tags: #stack #array #data-structure

## Stack
- Stack implements a **Last-in, First-out** or **LIFO** policy.
- It's also called as **First-in, Last-out** or **FILO** policy.
- *Insert* operation → **PUSH**
- *Delete* operation → **POP**

Think of a stack of books. You only have an access to the book on the top and you need to remove(pop) it to grab the next book.
So in Stack, delete operation removes the most recently added item in the set; hence it is called last-in, first-out.

### empty()

Returns `true` if a stack is empty else `false`.

```cpp
bool empty()
{
  return top == 0;
}
```

### push(x)

Inserts an element to the set. If `top == capacity`, print the error message that the set overflowed.

```cpp
void push(int val)
{
  if (top == capacity)
  {
    cout << "Overflow...";
    return;
  }

  top += 1;
  stack[top] = val;
}

```

### pop()

Removes an element from the stack. If `pop` is attempted when the stack is empty, print the error message that it underflowed.

```cpp
int pop() 
{
  if(empty())
  {
    cout << "Underflow...";
    return -1;
  }
  else
  {
    top -= 1;
    return stack[top + 1];
  }
}
```

[View](https://github.com/jioneeu/ds-algo/tree/master/stack/array/stack.cpp) full source code of Stack implementation using an array.


## Reference
- Introduction to Algorithms, 3rd Edition (CLRS)
