tags: #ruby 
related: [[210203 Basics pt.2]]

<hr />

## Variables
### local variables
A local variable should start with:
1. a lower case or an underscore
2. should contain upper or lower case letters, numbers, and underscore characters.
```rb
>> name = "Eubug"
>> name
=> "Eubug"

>> _valid = "hello";
>> _valid
=> "hello"

>> _myName = "EUBUG"
>> _myName
=> "EUBUG"
```


### global variables
A global variable starts with a `$`.

```rb
>> $PI = 3.14159
>> $PI
=> 3.14159
```

## Program flow
Ruby includes a standard set of looping and branching constructs: `if`, `while` and `case`.

### if-statements
```rb
# rand generates random number between 0 and 1
a = 10 * rand

if a < 5
	puts "#{a} less than 5"
elsif a > 7
	puts "#{a} greater than 7"
else
	puts "Cheese sandwich!"
end
```

### unless 
Ruby also supports a negated form of `if` called `unless`.

```rb
a = 10 * rand

unless a > 5
	puts "'a' less than or equal to 5"
else
	puts "'a' is greater than 5"
end
```

### one-liner
You can smash *if-statement* on one line. You use `if-then` format.
```rb
if a < 5 then puts "#{a} less than 5" end
if a < 5 then puts "#{a} less than 5" else puts "#{a} greater than 5" end
```

*if-statement* is also an expression. The last line of the block executed becomes its value.

```rb
puts(if a < 5 then puts "#{a} less than 5" else puts "#{a} greater than 5" end)
```

### *perl* style

Ruby has adopted the syntax from *Perl* where `if` and `unless` can be used as conditional modifiers *after* a statement.
```rb
puts "#{a} is less than 5" if a < 5

# print if a == 4
puts "Chees Sandwich!" unless a != 4
```

### while loop
`while` behaves as it does in other languages.
```rb
a = 10 * rand
while a > 5
	a = 10 * rand
end
```

There's also a negated version of `while` called `until` that loops the code *until* the condition is true.

The below code is identical to the one above.
```rb
a = 10 * rand
until a < 5
	a = 10 * rand
end
```

### case statements
A powerful version of the `if-elsif-else` system.

```rb
# outputs a random integer between 0 and 10
a = rand(11)

case a
when 0..5
	# if a == 0, 1, 2, 3, 4, or 5
	puts "#{a}: Low"
when 6
	puts "#{a}: Six"
else
	puts "#{a}: Cheese toast!"
end
```

## Writing functions
Functions are typically referred to as methods to keep Ruby's all-object-oriented-all-the-time design; there's no difference.

```rb
# file name: func1.rb
def greeting( name )
	puts "Hello, #{name}"
	return name.length
end

len = greeting("Eubug")
puts "My secret word is #{len} characters long"
```

Lets run the script.
```shell
$ ruby func1.rb
Hello, Eubug
My secret word is 5 characters long
```

Methods are defined by the `def` keyword, followed by the  function name.
Local and class methods should start with a lower case letter.
```rb
def function_name( [arg1, arg2, ...] )
end
```