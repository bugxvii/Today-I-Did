tags: #ruby #data-type 

<hr />

## Ruby Data Types
Ruby has 8 primitive types and 3 more data types derived from the Numeric superclass. Everything has a class in Ruby.

```rb
h = {"hash?" => "yep, it\'s a hash!", "the answer to everything" => 42, :linux => "fun for coders."}

puts "Stringy string McString!".class	# String
puts 1.class							# Fixnum
puts 1.class.superclass					# Integer
puts 1.class.superclass.superclass		# Numeric

puts 4.3.class							# Float
puts 4.3.class.superclass				# Numeric

puts nil.class							# NilClass
puts h.class							# Hash
puts :symbol.class						# Symbol
puts [].class							# Array
puts (1..8).class						# Range
```

Every object has a method called `class` that returns that object's class.

## Constants
1. Constants start with capital letters. 
	`Constant` is a constant.
	`constant` is NOT a constant.
2. You CAN change values of constants, but Ruby will give you a warning.

## Symbols
Ruby's object oriented ways have a cost => lots of objects slows down the program. Every time you type a string, Ruby makes a new object. It dosen't matter whether two strings are identical. Every instance is new.
```rb
irb> "live long and prosper".object_id
=> 180
irb> "live long and prosper".object_id
=> 200
```

You can see that the object ID returned by irb Ruby is different.

To get around this memory hoggishness, you can use *Symbols*.
`Symbol` is a lightweight object best used for comparisons and internal logic.
```rb
irb> :my_symbol.object_id
=> 2042268
irb> :my_symbol.object_id
=> 2042268
```
Symbols are denoted by the colon, like `:symbol_name`.

## Hashes
Hashes are like dictionaries. You have a *key*, a reference, and you *look it up* to find the associated object.

```rb
hash = { 
	:leia => "Princess from Alderaan",
	:han  => "Rebel without a cause",
	:luke => "Farmboy turned Jedi"
}

puts hash[:leia]	# Princess from Alderaan
puts hash[:han]		# Rebel without a cause
puts hash[:luke]	# Farmboy turned Jedi
```

Or we can also write it this way:
```rb
hash = { 
	:leia => "Princess from Alderaan",
	:han  => "Rebel without a cause",
	:luke => "Farmboy turned Jedi"
}

hash.each do |key, value|
	puts value
end
```

### delete
Maybe you want off Luke from the hash.
```rb
hash.delete(:luke)
```

Now Luke is no longer in the hash.

Or you can delete particular keys in general using `delete_if`. For example, you can delete all keys that contains the word *"farmboy"*
 
```rb
hash.delete_if { |key, value| value.downcase.match("farmboy") }
```

This iterates through each key-value pair and deletes one that matches the condition.

### add
We can add new key-value pair:
```rb
hash[:lando] = "Dashing and debonair city administrator."
```

### others
- `hash.length` => measure the hash
- `hash.keys` => display all keys in the hash as an array

## Reference
- https://en.wikibooks.org/wiki/Ruby_Programming/Data_types