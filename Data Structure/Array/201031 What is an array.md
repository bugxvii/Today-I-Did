tags: #array #data-structure #english 

<hr />

[[201031 배열(array)이란| 🇰🇷 한국어]]
[[201031 配列(Array)とは | 🇯🇵 日本語]]

## Array

Array is a container or a set which contains same type of variables. For example, in an integer array, only integers are allowed. In a character array, every data is a character.

![array](https://eubug.space/_next/image?url=https%3A%2F%2Fapi.super.so%2Fasset%2Feubug.space%2F53038785-88a3-4ca3-bd66-8c6d3fd29c73.png&w=1200&q=100)

We refer to each data in an array as an _element_ and the position each element is in is called the _index_.

In most programming languages, arrays use zero-based numbering meaning the first number starts from `0` and so on; negative indexes are not used (their are exceptions).

## Array Types

-   Linear array (1 dimension; see the picture above)
-   2D Array: array of an array (think of a cartesian plane)
-   3D Array: think of a rubik's cube
-   4D and above is also possible but it's not used that often due to its complexity.

## Arrays in Ruby

Ruby's array is also a set which composes of same _type_ variables but the difference is that this 'type' refers to the _Object;_ in an object array, only objects are allowed.

Almost everything in Ruby is object; thus, anything can be in an array.

For instance, we can have an array with a number, string, true/false, nil, or even an array since it's an object in Ruby.

![array2](https://eubug.space/_next/image?url=https%3A%2F%2Fapi.super.so%2Fasset%2Feubug.space%2Fac83e6b4-0444-43c6-8316-2569939988b3.png&w=1920&q=100)

Go ahead and run the code below to double check that all values are really an object.

```ruby
arr = [1, 3.2, "hello", true, [1,2,3], nil];

arr.each do |elem|
  puts elem.is_a? Object
end
```

## Operations

### create

We can use the literal constructor `[]` to create a new array.

```ruby
arr = []                    # => []
arr2 = [1, '2', "three"]    # => [1, '2', "three"]
```

Or we can explicitly call its `:new` method to create an array.

```ruby
arr = Array.new()      # => []
arr = Array.new(3)     # => [nil, nil, nil]
arr = Array.new(3, 0)  # => [0, 0, 0]
```

The first parameter refers to the size of a new array, and the second parameter is used to set the initial value of each element.

We need to be careful with using the 2nd parameter. When we use the 2nd parameter to create an array, Ruby populates an array that references the same object.

```ruby
# initial value is "hello"
arr = Array.new(3, "hello");     # => ["hello", "hello", "hello"]

arr[0].upcase!;   # do all-caps to the first 'hello'
puts arr          # => ["HELLO", "HELLO", "HELLO"] 
```

Since all elements reference the same object, changing the one element affects the every other elements as well.

So when we want to set the initial value using this method, it is recommended to use immutable objects (symbol, numbers, boolean, etc).

We can pass in blocks when we want to initialize each element with mutable objects.

```ruby
arr = Array.new(3) { "hello" }  # => ["hello", "hello", "hello"]

arr[0].upcase!
puts arr            # => ["HELLO", "hello", "hello"]
```

And finally, we can use `[Array()](<https://ruby-doc.org/core-2.7.0/Kernel.html#method-i-Array>)` method which is provided by the kernel.

```ruby
Array([])            # => []
Array(nil)           # => []
Array([1, 2, 3])     # => [1, 2, 3]
Array(1..5)          # => [1, 2, 3, 4, 5]
Array(1...5)         # => [1, 2, 3, 4]

```

### access

In the beginnig, I said 0 or natural numbers are used for array's index. In Ruby, however, negative indexing is also possible.

Negative indexes start counting from the end.

```ruby
arr = [1, 2, 3, 4, 5]
arr[2]    # => 3
arr[1]    # => 2
arr[0]    # => 1
arr[-1]   # => 5
arr[-2]   # => 4
arr[100]  # => nil
```

Ruby returns `nil` when we try to access outside of the array bounds like `arr[100]` in size 5 array. In order to raise 'out of bounds' error, we can use `:fetch` method.

```ruby
arr = [1, 2, 3, 4, 5]
arr.fetch(0)            # => 1
arr.fetch(100)          # => IndexError (index 100 outside of array bounds: -5...5)
arr.fetch(100, 'out!')  # => "out!"
```

### insert

We can use `:push` and `:<<` to insert an element at the end of an array.

```ruby
arr = [1]
arr.push(2)  # => [1, 2]
arr << 3     # => [1, 2, 3]
```

To insert an element at the beginning, we use `:unshift`.

```ruby
arr = [3]
arr.unshift(2)  # => [2, 3]
arr.unshift(1)  # => [1, 2, 3]
```

Or we can use `:insert` to insert an element anywhere in the array.

```ruby
arr = ['one', 'two', 'four', 'five']
arr.insert(2, 'three')   # => ["one", "two", "three", "four", "five"]
```

### delete

We can use `:pop` and `:shift` method to delete an element at the end and at the beginning, respectively.

```ruby
arr = [1, 2, 3, 4, 5]
a.pop    # => 5
arr      # => [1, 2, 3, 4]

a.shift  # => 1
arr      # => [2, 3, 4]
```

To delete an element at a specific position, use `:delete_at`.

```ruby
arr = [1, 2, 3, 4, 5]
arr.delete_at(2)    # => 3
arr                 # => [1, 2, 4, 5]
```

To delete all elements with a specific value, use `:delete`.

```ruby
arr = [1, 2, 2, 3, 4]
arr.delete(2)  # => 2
arr            # => [1, 3, 4]
```

Lastly, we can use this special method `:uniq` to remove all duplicates in the array.

```ruby
arr = [1, 2, 2, 3, 3, 3, 4, 5, 5]
arr.uniq  # => [1, 2, 3, 4, 5]
arr       # => [1, 2, 2, 3, 3, 3, 4, 5, 5]

arr.uniq! # => [1, 2, 3, 4, 5]
arr       # => [1, 2, 3, 4, 5] 
```

## 2D Array

Let's briefly take a look at the structure of 2D Array and how to create one in Ruby.

![2d array](https://eubug.space/_next/image?url=https%3A%2F%2Fapi.super.so%2Fasset%2Feubug.space%2F929c58be-6055-44c4-b7dd-ef27c5f6d48f.png&w=1080&q=100)

Unlike the linear array where we used one index to access its element, we need 2 indexes (row, column) to access elements in 2D arrays.

Remember that the order of the index is `arr[row][col]` not `arr[col][row]` (see the picture above).

### ways to create a 2d array

![2d array 2](https://eubug.space/_next/image?url=https%3A%2F%2Fapi.super.so%2Fasset%2Feubug.space%2F85ce543e-53ec-4be9-aae0-ec2b32a1ca63.png&w=1080&q=100)

1.  Hard coding.
    
    ```ruby
    arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    
    arr[0]     # => [1, 2, 3]
    arr[1]     # => [4, 5, 6]
    arr[2]     # => [7, 8, 9]
    arr[0][1]  # => 2
    arr[2][2]  # => 9
    ```
    
2.  Using a `:new` method.
    
    We can create a linear array using the `:new` method and insert sub-arrays as an element to create a 2D array.
    
    ```ruby
    arr = Array.new(3)  # => [nil, nil, nil]
    
    arr[0] = [1, 2, 3]  # => [[1,2,3], nil, nil]
    arr[1] = [4, 5, 6]  # => [[1,2,3], [4,5,6], nil]
    arr[2] = [7, 8, 9]  # => [[1,2,3], [4,5,6], [7,8,9]]
    ```
    
3.  Or we can pass in blocks to create a 2D array from the start.
    
    ```ruby
    arr = Array.new(3) { [] }  # => [[], [], []]
    
    arr[0] << 1   # => [[1], [], []]
    arr[1] << 4   # => [[1], [4], []]
    arr[2] << 7   # => [[1], [4], [7]]
    ```
    

In Ruby, multi-dimensional array is really just an array with its element being an array. So all operations used in 1D array can also be used in higher dimensional arrays.