# Solutions to Easy Questions - Quiz 3

## Exercise 1

### Question
If we have this code:

```
class Greeting
  def greet(message)
    puts message
  end
end

class Hello < Greeting
  def hi
    greet("Hello")
  end
end

class Goodbye < Greeting
  def bye
    greet("Goodbye")
  end
end
```

What happens in each of the following cases:

#### case 1:

```
hello = Hello.new
hello.hi
```

#### answer
'Hello' is printed

#### case 2:

```
hello = Hello.new
hello.bye
```

#### answer
There is an undefined method error, because hello cannot find a method called bye on its lookup path.

#### case 3:

```
hello = Hello.new
hello.greet
```

#### answer
There is an ArgumentError for the wrong number of arguments since the greet method expects a message as an argument.

#### case 4:

```
hello = Hello.new
hello.greet("Goodbye")
```

#### answer
'Goodbye' is printed

#### case 5:

```
Hello.hi
```

#### answer
There is an undefined method error because there is no class method called hi for the Hello class.

## Exercise 2

### Question
In the last question we had the following classes:

```
class Greeting
  def greet(message)
    puts message
  end
end

class Hello < Greeting
  def hi
    greet("Hello")
  end
end

class Goodbye < Greeting
  def bye
    greet("Goodbye")
  end
end
```

If we call Hello.hi we get an error message. How would you fix this?

### Answer
Change the hi method in the hello class to be a class method instead of an instance method by adding self to the method definition. Additionally, you have to create a new object of the Greeting class inside of the method and then use its greet call.

```
class Hello < Greeting
  def self.hi
    greeting = Greeting.new
    greeting.greet("Hello")
  end
end
```

## Exercise 3

### Question
When objects are created they are a separate realization of a particular class.

Given the class below, how do we create two different instances of this class, both with separate names and ages?

```
class AngryCat
  def initialize(age, name)
    @age  = age
    @name = name
  end

  def age
    puts @age
  end

  def name
    puts @name
  end

  def hiss
    puts "Hisssss!!!"
  end
end
```

### Answer
Just define two objects using the new method and passing in different variables:

```
alia = AngryCat.new(5, 'Alia')
ziggy = AngryCat.new(1, 'Ziggy')
```

## Exercise 4

### Question
Given the class below, if we created a new instance of the class and then called to_s on that instance we would get something like "#<Cat:0x007ff39b356d30>"

```
class Cat
  def initialize(type)
    @type = type
  end
end
```

How could we go about changing the to_s output on this method to look like this: I am a tabby cat? (this is assuming that "tabby" is the type we passed in during initialization).

### Answer
Add a new to_s method to the class that will override the existing method:

```
class Cat
  attr_reader :type

  def initialize(type)
    @type = type
  end

  def to_s
  	puts "I am a #{type} cat"
  end
end
```

## Exercise 5

### Question
If I have the following class:

```
class Television
  def self.manufacturer
    # method logic
  end

  def model
    # method logic
  end
end
```

What would happen if I called the methods like shown below?

```
tv = Television.new
tv.manufacturer
tv.model

Television.manufacturer
Television.model
```

### Answer
You would get an error for tv.manufacturer (undefined method) because the manufacturer method is only defined for the class (not an instnace of the class). Similarily, Television.model would also return an error because the model method is only defined for instances of the class Television, not the class itself.

## Exercise 6

### Question
If we have a class such as the one below:

```
class Cat
  attr_accessor :type, :age

  def initialize(type)
    @type = type
    @age  = 0
  end

  def make_one_year_older
    self.age += 1
  end
end
```

In the make_one_year_older method we have used self. What is another way we could write this method so we don't have to use the self prefix.

### Answer
You can replace self with @ to refer to the instance variable directly, so it would be @age += 1.

## Exercise 7

### Question
What is used in this class but doesn't add any value?

```
class Light
  attr_accessor :brightness, :color

  def initialize(brightness, color)
    @brightness = brightness
    @color = color
  end

  def self.information
    return "I want to turn on the light with a brightness level of super high and a colour of green"
  end

end
```

### Answer
You don't need return in the self.information method because Ruby will automatically return the last line of the method.