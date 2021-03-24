tags: #ruby #data-type #english
related: [[210204 Data types pt.1]] | [[210206 Data types pt.3]]

<hr />

## Ruby Data Types
## Arrays
`Arrays` are a lot like `Hash` except that the keys are always consecutive numbers, and always starts at 0.

### creation of an array
There are two ways to create an array in Ruby:
```rb
array1 = ["hello", "this", "is", "an", "array!"]
array2 = []
```

### insertion
We can use `<<` operator to insert an item to the array.
```rb
array2 = []
array2 << "This"   # index 0
array2 << "is"     # index 1
array2 << "also"   # index 2
array2 << "an"     # index 3
array2 << "array!" # index 4
```

### deletion
To remove an item from the array, use `Array.pop`.
```rb
string = array2.pop
puts string  # array!
```

### empty?
If you continuously *pop* an element from the array, eventually the array will be empty. We can check the emptiness using `Arary.empty?` and use this in the loop to move all elements from one `Array` to another.

```rb
array1 << array2.pop until array2.empty?
```

### set operations
Ruby's array supports basic set operations like *union* and *difference*.
```rb
array3 = array1 + array2 # union
array4 = array1 - array2 # difference
```

- `arary3` -> contains all the elements of both `array1` and `array2`
- `array4` -> contains all of the elements that `array1` did, except for the ones that were also in `array2`

You can turn `Array` into a `String`:
```rb
arr = ["my", "name", "is", "Eubug"]
console.log( arr.join("") ) # mynameisEubug
console.log( arr.join(" ") ) # my name is Eubug

```

## Reference
- https://en.wikibooks.org/wiki/Ruby_Programming/Data_types#Arrays