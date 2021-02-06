tags: #ruby #data-type 
related: [[210204 Data types pt.1]] | [[210205 Data types pt.2]] 

<hr />

## Ruby Data Types
## Strings
In Ruby, you can multiple `string`:
```rb
"Danger!" * 5  # Danger!Danger!Danger!Danger!Danger!
```

You can also compare strings:
```rb
"a" < "b" # true
```

When comparing characters in the string, it's actually comparing the ASCII values.
You can use `String.ord` or `?` operator to find character's ASCII value. For more details, check the previous note about [[210129 ASCII | ASCII]].

## Integer.chr
To perform the opposite conversion (from ASCII to a character), use `Integer.chr` method.

```rb
puts 65.chr # A
puts 97.chr # a
```

## String.scan
To iterate through each characters in a `String` object, use `String.scan`:
```rb
thing = "Red fish"
thing.scan(/./) { |letter| puts letter }
```
yields
```shell
R
e
d

f
i
s
h
```

### regular expression
So what is this weird `/./` thing in the parameter? This is called a [regular expression](https://en.wikibooks.org/wiki/Ruby_Programming/Reference/Objects/Regexp). So in *"regex"* language, `/./` means *"any one character"*.

There's also a `=~` operator or *match operator* in Ruby. We can use this operator to check whether the `String` matches a given regex.

```shell
>> puts "Yes, there's a number" if "My name is Eubug! <3" =~ /[0-9]/
Yes, there's a number
=> nil
```

The `String.match` works the same way except it can accept a `String` as a parameter.

```rb
>> string = "My name is Eubug"
>> string.match("Eubug")
=> #<MatchData "Eubug">
>> string.match("hello")
=> nil
```

## String.sub
We can replace a word in a string using the `String.sub` method.
```rb
string1 = "2 + 2 = 4"
string2 = string1.sub("4", "5")	# 2 + 2 = 5
```

`String.sub` only replaces the first occurrence of a word. In order to replace *all* occurrences, use `String.gsub` which means *"global substitute"*:

```rb
string = "He is dangerous! dangerous! dangerous!"
string.gsub("dangerous", "lovely")

puts string # He is lovely! lovely! lovely!
```

## Additional String Methods
```rb
\# Outputs 1585761545
"Mary J".hash

\# Outputs "concatenate"
"concat" + "enate"

\# Outputs "Washington"
"washington".capitalize

\# Outputs "uppercase"
"UPPERCASE".downcase

\# Outputs "LOWERCASE"
"lowercase".upcase

\# Outputs "Henry VII"
"Henry VIII".chop

\# Outputs "rorriM"
"Mirror".reverse

\# Outputs 810
"All Fears".sum

\# Outputs cRaZyWaTeRs
"CrAzYwAtErS".swapcase

\# Outputs "Nexu" (next advances the word up one value, as if it were a number.)
"Next".next

\# After this, nxt == "Neyn" (to help you understand the trippiness of next)
nxt \= "Next"
20.times {nxt \= nxt.next}
```