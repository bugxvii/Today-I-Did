tags: #ruby #data-type 

---

## Method definition
A method starts with the `def` keyword and ended with the `end`.

```rb
def myMethod
	# something
end
```

You can define a method that takes parameters by providing its name of the variable in parentheses after the method name.

```rb
def myMethod(arg1, arg2, ..., argN)
	puts arg1;
	puts arg2;
end
```

## Invoking methods
You can invoke methods with or without parentheses but it's a good practice to put parentheses to differentiate it from other variables.

```rb
def add(a, b)
	puts a + b
end

add(1, 2) # 3
add 1, 2  # 3
add("abc", "xyz") # abcxyz
```

## Default values
We can assign a default value in the definition.

```rb
def myMethod(message="This is a default value")
	puts message
end
	
myMethod();
myMethod("Where has the default value gone?");
```

## Returning values

You can return a value from the method using `return`.
```rb
def myMethod
	return "Return!"
end

puts myMethod # Return!
```

But the below code will work too:
```rb
def myMethod
	"This also works!!"
end

puts myMethod # This also works!!
```

The reason for this is that Ruby always returns the last evaluated statement.