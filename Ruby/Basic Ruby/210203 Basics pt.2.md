tags: #ruby 
related: [[210201 Basics pt.1]]

## Blocks
Ruby's code block has some secret powers.

You can define code blocks in Ruby either with curly brackets `{..}` or `do..end` keyword.

```rb
do
	print "My name is "
	print "Eubug!"
end

{
	print "Nice to meet you!"
}
```

You can pass in code block as a parameter in Ruby.

```rb
$ irb --simple-prompt
>> 3.times { puts "Hi" }
Hi!
Hi!
Hi!
=> 3
```

We just passed `{ puts "Hi" }` block as a parameter for `n.times` function.
`times` function will pass the control over to the block and it executes `puts`, then it returns the control back to `times` and repeat this for `3` times.

### Blocks with a parameter
Blocks can receive a parameter from the function using a special notation `|..|`.
```rb
irb --simple-prompt
>> 4.times { |x| puts "Loop number #{x}" }
Loop number 0
Loop number 1
Loop number 2
Loop number 3
=> 4
```

Here, `times` function passes a number into the block and we're receiving that number from user-defined variable `x`.

### yield
Functions interact with blocks through the `yield`. Every time the function invokes `yield` control passes to the block and return once the block is finished.

```rb
# file name: block.rb
def language
  yield
  yield
end

language  { puts "I like language!" }
```

```shell
$ ruby block.rb
I like language!
I like language!
```

Another example where the function passes a parameter to the block:

```rb
def language
  yield "C++"
  yield "Ruby"
  yield "JavaScript"
end

language { |x| puts "I like #{x}"}
puts
language { |x| puts "#{x} is #{x.length} characters long!"}
```

```shell
$ ruby language
I like C++
I like Ruby
I like JavaScript

C++ is 3 characaters long!
Ruby is 4 characters long!
JavaScript is 10 characters long!
```

## Ruby is really, really object-oriented
In Ruby everything is an object. As you saw it from earlier, a number like `3` is also an object. Otherwise, it wouldn't be possible to call a function like this:
```rb
3.times { puts "Hi!" }
```

`3` might seem like just a constant number but it's in fact an instance of the class *Fixnum*.