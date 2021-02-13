tags: #ruby #object #english

<hr />

Ruby is a pure object-oriented language.

## What is an object?
An object can do exactly three things:
1. An object can contain data, including references to other objects (* pointer *).
2. An object can contain methods, which are functions that have special access to the object's data.
3. An object's methods can call/run other methods/functions.

## Variables and objects
```shell
$ irb --simple-prompt
>> language = "Ruby"
=> Ruby
```

We created an object `language` which holds (or points to ) the string `"Ruby"`.

Now let's create another variable and let it refer to the same String object as `language`.

```rb
>> favorite_language = language
=> Ruby
```

Now, we have two variables `language` and `favorite_language` that we can use to refer to the same String object, `"Ruby"`. If we change this String object from `language`, we can also view the change from `favorite_language`.

## Methods
In Ruby, methods that end with an exclamation mark (also called "bang") modify the object itself.

```rb
>> language.upcase!
=> "RUBY"
```

Since both variables (`language` and `favorite_language`) point to the same object, we can see the uppercase text using either variable.
```rb
>> language
=> "RUBY"
>> favorite_language
=> "RUBY"
```

Methods without the bang, will return data but do not modify the object.
```rb
>> language.downcase
=> "ruby"
>> language
=> "RUBY"
```

## Reassigning a variable
Your favorite language may not be `"Ruby"`. So let's change it.
```rb
>> favorite_language = "C++"
=> "C++"
```

Now each variable points to a different String object.
- `language` ---> `"Ruby"`
- `favorite_language` ---> `"C++"`

Let say now your favorite language is something else.
```rb
>> favorite_language = "something"
=> "something"
```

Now no variable refers to the String object `"C++"`, so Ruby will dispose of it.

## Pitfalls
```rb
>> language = "Ruby"
=> "Ruby"
>> favorite_language = "Ruby"
=> "Ruby"
```

Although two strings have same characters, they are two **different String objects**. 
```rb
>> language.upcase!
=> "RUBY"
>> favorite_language
=> "Ruby"
```

## Reference
- https://en.wikibooks.org/wiki/Ruby_Programming/Introduction_to_objects