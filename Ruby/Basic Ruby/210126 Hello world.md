tags: #ruby #english

## Hello World
Create a `hello.rb` file and type the following:
```rb
puts 'Hello, world!'
```

run this code by
```sh
$ ruby hello.rb
Hello, world!
```

You can use the `-e` flag to run the short code directly from the terminal. Don't forget the wrapping quotes (`""`).
```sh
$ ruby -e "puts 'Hello, world!'"
Hello, world!
```

## Comments
### One-line comments
```rb
# this is a comment
# puts "this wont be printed"

puts "Hello!"
```

### Multiline comments
```rb
=begin
This is a multi-
line comments!
puts "Hello!"
=end

puts "World!"
```

## Executable ruby scripts
You always need to use `ruby` to run the script.
To omit this command we can do the following:
1. make your file executable (`chmod u+x hello.rb`)
2. add a *[shebang](https://en.wikibooks.org/wiki/Ruby_Programming/Hello_world)* line (`#!/usr/bin/env ruby`)

And now we can just run the script like this
```bash
$ ./hello
```

If your script is something that you use daily, you can move it to `~/bin` directory and just call its name to run the script (`hello.rb`) just like other programs like `bash`, `vim`, and so on...

## Reference
- https://en.wikibooks.org/wiki/Ruby_Programming/Hello_world