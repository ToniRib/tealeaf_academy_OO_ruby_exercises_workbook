# Solutions to Easy Questions - Quiz 2

## Exercise 1

### Question
You are given the following code:

```
class Oracle
  def predict_the_future
    "You will " + choices.sample
  end

  def choices
    ["eat a nice lunch", "take a nap soon", "stay at work late"]
  end
end
```

What is the result of calling

```
oracle = Oracle.new
oracle.predict_the_future
```

### Answer
You will get one of the three strings in the array inside of the choices method with "You will " on the front of it. The string will be chosen at random.

## Exercise 2

### Question
We have an Oracle class and a RoadTrip class that inherits from the Oracle class.

```
class Oracle
  def predict_the_future
    "You will " + choices.sample
  end

  def choices
    ["eat a nice lunch", "take a nap soon", "stay at work late"]
  end
end

class RoadTrip < Oracle
  def choices
    ["visit Vegas", "fly to Fiji", "romp in Rome"]
  end
end
```

What is the result of the following:

```
trip = RoadTrip.new
trip.predict_the_future
```

### Answer
You will get a string in the form "You will " plus one of the choices from the RoadTrip class because the choices method there overrides the choices method in the Oracle class.

## Exercise 3

### Question
How do you find where Ruby will look for a method when that method is called? How can you find an object's ancestors?

```
module Taste
  def flavor(flavor)
    puts "#{flavor}"
  end
end

class Orange
  include Taste
end

class HotSauce
  include Taste
end
```

What is the lookup chain for Orange and HotSauce?

### Answer
Ruby will start at the current class then work through the ancestory lookup chain. To figure out what the ancestors of a particular class are you can use the ancestors method.

The ancestors for Orange are:

```
Orange.ancestors
=> [Orange, Taste, Object, Kernel, BasicObject]
```

The ancestors for HotSauce are:

```
HotSauce.ancestors
=> [HotSauce, Taste, Object, Kernel, BasicObject]
```

## Exercise 4

### Question
What could you add to this class to simplify it and remove two methods from the class definition while still maintaining the same functionality?

```
class BeesWax
  def initialize(type)
    @type = type
  end

  def type
    @type
  end

  def type=(t)
    @type = t
  end

  def describe_type
    puts "I am a #{@type} of Bees Wax"
  end
end
```

### Answer
You can add attr_accessor and also then change @type to just type in the describe_type method.

```
class BeesWax
  attr_accessor :type

  def initialize(type)
    @type = type
  end

  def describe_type
    puts "I am a #{type} of Bees Wax"
  end
end
```

## Exercise 5

### Question
There are a number of variables listed below. What are the different types and how do you know which is which?

```
excited_dog = "excited dog"
@excited_dog = "excited dog"
@@excited_dog = "excited dog"
```

### Answer
excited_dog is a local variable because it has no @.
@excited_dog is an instance variable because it has a @ prefix.
@@excited_dog is a class variable because it has a @@ prefix.

## Exercise 6

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

Which one of these is a class method (if any) and how do you know? How would you call a class method?

### Answer
The class method is self.manufacturer because it uses the self keyword in the method definition. You can call this method directly on the class itself, such as:

```
Television.manufacturer
```

## Exercise 7

### Question
If we have a class such as the one below:

```
class Cat
  @@cats_count = 0

  def initialize(type)
    @type = type
    @age  = 0
    @@cats_count += 1
  end

  def self.cats_count
    @@cats_count
  end
end
```

Explain what the @@cats_count variable does and how it works. What code would you need to write to test your theory?

### Answer
The @@cat_counts variable is a class variable (denoted by the @@ prefix) and it counts the number of Cat objects that have been instantiated. In order to test this, you could write something like this:

```
cat1 = Cat.new('black')
Cat.cats_count 		=> 1
cat2 = Cat.new('tabby')
Cat.cats_count 		=> 2
cat3 = Cat.new('longhair')
Cat.cats_count 		=> 3
```

## Exercise 8

### Question
If we have this class:

```
class Game
  def play
    "Start the game!"
  end
end
```

And another class:

```
class Bingo
  def rules_of_play
    #rules of play
  end
end
```

What can we add to the Bingo class to allow it to inherit the play method from the Game class?

### Answer
Add '< Game' after the Bingo class definition to indicate that it will inherit from the Game class, thus making all of the Game methods available.

```
class Bingo < Game
  def rules_of_play
    #rules of play
  end
end
```

## Exercise 9

### Question
If we have this class:

```
class Game
  def play
    "Start the game!"
  end
end

class Bingo < Game
  def rules_of_play
    #rules of play
  end
end
```

What would happen if we added a play method to the Bingo class, keeping in mind that there is already a method of this name in the Game class that the Bingo class inherits from.

### Answer
If you then called the play method from an object of the Bingo class, it would use the Bingo class method for play, not the Game method for play.

## Exercise 10

### Question
What are the benefits of using Object Oriented Programming in Ruby? Think of as many as you can.

### Answer

- Associate behaviors with objects
- Allows you to think more abstractly about a problem
- Gives a nice way to DRY out the code by using inheritance and mixins
- Allows for more complex programs
- Can reuse code more easily
