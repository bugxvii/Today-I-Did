tags: #ruby 

<hr />

# Strings
## String literals
We can create a string literal using single or double quotes.
```ruby
puts 'Hello world'
puts "Hello world"
```

There's not much of difference between single and double quotes in Ruby. However, take a look at the following code:
```ruby
puts "Betty's pie shop"
puts 'Betty\'s pie shop'
```

When a double quote is used, we can simply add apostrophe with no issue. With single quotes, however, we need *escape sequence* to tell the program that this single quote is part of the string.

## Single quotes
Supports only 2 escape sequences
-  `\'` - single quote
- `\\` - single backslash

Everything else between single quotes is treated literally.

## Double quotes
You can escape more sequences than single quotes. It also allows you to embed variables or expressions in string literals (*interpolation*)

### escape sequences
-  `\'` - single quote
- `\\` - single backslash
- `\a` - bell/alert
- `\b` - backspace
- `\r` - carriage return
- `\n` - newline
- `\s` - space
- `\t` - tab

### string interpolation
```ruby
name = "Eubug"
puts "Hello my name is #{name}" 
# Hello my name is Eubug
```

## puts & print
- `puts` automatically attach `\n` at the end.
- `print` does not.
```rb
puts "Hello", "World"
## Hello
## World

print "Hello", "World"
## HelloWorld
```

<hr />

# Alternative quotes
There's more than one way to quote string literals in Ruby.
- `%q` operator: `%q(abc)` == `'abc'`
- `%Q` operator: `%Q(abc's)` == `"abc's"`

## alternate single quotes
Let's say we're trying to print out the following path:

```rb
puts 'c:\\bus schedules\\napolean\\the portland bus schedule.txt'
```

There are couple issues here. 
- `\b` in `\c:\\bus`
- `\n` in `\napolean`
- `\t` in `\the`

These will be treated as escape sequences. We can use our alternate single quote method and choose our own *delimiter* which marks the beginning and end of the string literal.
```rb
puts %q(c:\\bus schedules\\napolean\\the portland bus schedule.txt)
puts %q!c:\\bus schedules\\napolean\\the portland bus schedule.txt!
puts %q^c:\\bus schedules\\napolean\\the portland bus schedule.txt^
puts %q{c:\\bus schedules\\napolean\\the portland bus schedule.txt}
puts %q<c:\\bus schedules\\napolean\\the portland bus schedule.txt>
puts %q/c:\\bus schedules\\napolean\\the portland bus schedule.txt/
puts %q#c:\\bus schedules\\napolean\\the portland bus schedule.txt#
```

But if your delimiter shows up as a string inside the quote, you need to escape it.
- Exceptions: you don't need to escape sequence when using matching braces.

## alternate double quotes
It works much the same as the `%q` operator.
Since this is a double quote, you can use string interpolation.

```rb
name = "napoleon"
puts %Q(c:\\bus schedules\\#{name}\\the portland bus schedule.txt)
name = "eubug"
puts %Q(c:\\bus schedules\\#{name}\\the portland bus schedule.txt)
```

## Reference
- https://en.wikibooks.org/wiki/Ruby_Programming/Strings