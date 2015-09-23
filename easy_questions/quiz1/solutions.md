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

## Exercise 2

### Question
If we have a Car class and a Truck class and we want to be able to go_fast, how can we add the ability for them to go_fast using the module Speed. How can you check if your Car or Truck can now go fast?

```
module Speed
  def go_fast
    puts "I am a #{self.class} and going super fast!"
  end
end

class Car
  def go_slow
    puts "I am safe and driving slow."
  end
end

class Truck
  def go_very_slow
    puts "I am a heavy truck and like going very slow."
  end
end
```

### Answer
You can include the Speed module as a mixin and then test it by instantiating both a car and a truck object and then calling the go_fast method on them.

```
class Car
  include Speed

  def go_slow
    puts "I am safe and driving slow."
  end
end

class Truck
  include Speed

  def go_very_slow
    puts "I am a heavy truck and like going very slow."
  end
end

car = Car.new
car.go_fast
truck = Truck.new
truck.go_fast
```

## Exercise 3

### Question
When we called the go_fast method from an instance of the Car class (as shown below) you might have noticed that the string printed when we go fast includes the name of the type of vehicle we are using. How is this done?

```
>> small_car = Car.new
>> small_car.go_fast
I am a Car and going super fast!
```

### Answer
The go_fast method calls self.class, but since go_fast is called on the small_car object, that actually means small_car.class, which of course was created from the Car class!

## Exercise 4

### Question
If we have a class AngryCat how do we create a new instance of this class?

The AngryCat class might look something like this:

```
class AngryCat
  def hiss
    puts "Hisssss!!!"
  end
end
```

### Answer
Create a new instance of the AngryCat by using the new method:

```
mr_fuzzy = AngryCat.new
```

## Exercise 5

### Question
Which of these two classes has an instance variable and how do you know?

```
class Fruit
  def initialize(name)
    name = name
  end
end

class Pizza
  def initialize(name)
    @name = name
  end
end
```

### Answer
Pizza has an instance variable because it uses the @ sign in the initialize method which denotes an instance variable.

## Exercise 6

### Question
What could we add to the class below to access the instance variable @volume?

```
class Cube
  def initialize(volume)
    @volume = volume
  end
end
```

### Answer
Add the attr_reader to be able to read the volume:

```
class Cube
  attr_reader :volume

  def initialize(volume)
    @volume = volume
  end
end
```

## Exercise 7

### Question
What is the default thing that Ruby will print to the screen if you call to_s on an object? Where could you go to find out if you want to be sure?

### Answer
Ruby will print out the object's class and an encoded version of its object id. You can hop into irb to find out for sure.

## Exercise 8

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

You can see in the make_one_year_older method we have used self. What does self refer to here?

### Answer
The instance variable age for the calling object.

For example:

```
alia = Cat.new('black')
alia.make_one_year_older
alia.age
```

In this case, the calling object is the alia object, which is of the class Cat, so self refers to alia.

## Exercise 9

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

In the name of the cats_count method we have used self. What does self refer to in this context?

### Answer
It refers to the class Cat. You could use it in this way:

```
alia = Cat.new('black')
ziggy = Cat.new('tabby')
Cat.cats_count 					=> 2
```

## Exercise 10

### Question
If we have the class below, what would you need to call to create a new instance of this class?

```
class Bag
  def initialize(color, material)
    @color = color
    @material = material
  end
end
```

### Answer

```
my_bag = Bag.new('brown', 'cloth')
```
