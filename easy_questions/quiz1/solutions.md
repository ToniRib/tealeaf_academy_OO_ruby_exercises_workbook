# Solutions to Easy Questions - Quiz 1

## Exercise 1

### Question
Which of the following are objects in Ruby? If they are objects, how can you find out what class they belong to?

```
true
"hello"
[1, 2, 3, "happy days"]
142
```

### Answer
They are all objects! You can find out what class they belong to by using the class method, such as:

```
true.class 						=> TrueClass
"hello".class 					=> String
[1, 2, 3, "happy days"].class 	=> Array
142.class 						=> Fixnum
```