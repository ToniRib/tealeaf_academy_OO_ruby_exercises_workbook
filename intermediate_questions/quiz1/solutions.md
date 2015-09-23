# Solutions to Intermediate Questions - Quiz 1

## Exercise 1

### Question
Ben asked Alyssa to code review the following code:

```
class BankAccount
  attr_reader :balance

  def initialize(starting_balance)
    @balance = starting_balance
  end

  def positive_balance?
    balance >= 0
  end
end
```

Alyssa glanced over the code quickly and said - "It looks fine, except that you forgot to put the @ before balance when you refer to the balance instance variable in the body of the positive_balance? method."

"Not so fast", Ben replied. "What I'm doing here is valid - I'm not missing an @!"

Who is right, Ben or Alyssa, and why?

### Answer
Ben, because he used the attr_reader to create the getter method for balance, so he can use balance without the @ in his code. The balance inside of positive_balance? is actually using this getter method to return the instance variable @balance.

## Exercise 2

### Question
Alyssa created the following code to keep track of items for a shopping cart application she's writing:

```
class InvoiceEntry
  attr_reader :quantity, :product_name

  def initialize(product_name, number_purchased)
    @quantity = number_purchased
    @product_name = product_name
  end

  def update_quantity(updated_count)
    # prevent negative quantities from being set
    quantity = updated_count if updated_count >= 0
  end
end
```

Alan looked at the code and spotted a mistake. "This will fail when update_quantity is called", he says.

Can you spot the mistake and how to address it?

### Answer
The quantity value needs a setter method, which should be initialized with attr_accessor instead of attr_reader if Alyssa wants to call quantity inside of the update_quantity method without using the @ sign. If she changes attr_reader to attr_accessor, she can then change quantity to self.quantity and it will work.

```
class InvoiceEntry
  attr_reader :product_name
  attr_accessor :quantity

  def initialize(product_name, number_purchased)
    @quantity = number_purchased
    @product_name = product_name
  end

  def update_quantity(updated_count)
    # prevent negative quantities from being set
    self.quantity = updated_count if updated_count >= 0
  end
end
```

## Exercise 3

### Question
In the last question Alyssa showed Alan this code which keeps track of items for a shopping cart application:

```
class InvoiceEntry
  attr_reader :quantity, :product_name

  def initialize(product_name, number_purchased)
    @quantity = number_purchased
    @product_name = product_name
  end

  def update_quantity(updated_count)
    quantity = updated_count if updated_count >= 0
  end
end
```

Alan noticed that this will fail when update_quantity is called. Since quantity is an instance variable, it must be accessed with the @quantity notation when setting it. One way to fix this to change attr_reader to attr_accessor.

Is there anything wrong with fixing it this way?

### Answer
If you change attr_reader to attr_accessor, it will allow people to set the quantity directly using a notation like:

```
invoice = InvoiceEntry.new('apples', 2)
invoice.quantity = 4
```

instead of going through the update_quantity method, thereby circumventing the checks that are in the update_quantity method.

## Exercise 4

### Question
Let's practice creating an object hierarchy.

Create a class called Greeting with a single method called greet that takes a string argument and prints that argument to the terminal.

Now create two other classes that are derived from Greeting: one called Hello and one called Goodbye. The Hello class should have a hi method that takes no arguments and prints "Hello". The Goodbye class should have a bye method to say "Goodbye". Make use of the Greeting class greet method when implementing the Hello and Goodbye classes - do not use any puts in the Hello or Goodbye classes.

### Answer
See file: greetings.rb

## Exercise 5

### Question
You are given the following class that has been implemented:

```
class KrispyKreme
  def initialize(filling_type, glazing)
    @filling_type = filling_type
    @glazing = glazing
  end
end
```

And the following specification of expected behavior:

```
donut1 = KrispyKreme.new(nil, nil)
donut2 = KrispyKreme.new("Vanilla", nil)
donut3 = KrispyKreme.new(nil, "sugar")
donut4 = KrispyKreme.new(nil, "chocolate sprinkles")
donut5 = KrispyKreme.new("Custard", "icing")

puts donut1
  => "Plain"

puts donut2
  => "Vanilla"

puts donut3
  => "Plain with sugar"

puts donut4
  => "Plain with chocolate sprinkles"

puts donut5
=> "Custard with icing"
```

Write additional code for KrispyKreme such that the puts statements will work as specified above.

### Answer

See file: krispy_kreme.rb

## Exercise 6

### Question
If we have these two methods:

```
class Computer
  attr_accessor :template

  def create_template
    @template = "template 14231"
  end

  def show_template
    template
  end
end
```

and

```
class Computer
  attr_accessor :template

  def create_template
    self.template = "template 14231"
  end

  def show_template
    self.template
  end
end
```

What is the difference in the way the code works?

### Answer
In the first example, the show_template method is calling the getter method template defined with the attr_accessor statement to get the instance variable @template. In the second example, it is getting the instance variable directly without referencing the getter method. The first example is better because it doesn't call self unnecessarily.

## Exercise 7

### Question
How could you change the method name below so that the method name is more clear and less repetitive.

```
class Light
  attr_accessor :brightness, :color

  def initialize(brightness, color)
    @brightness = brightness
    @color = color
  end

  def self.light_information
    "I want to turn on the light with a brightness level of super high and a colour of green"
  end
end
```

### Answer
Get rid of the light_ in the light_information method so it reads just 'self.information' which is much simpler. You could also just use the recognizeable shorthand 'self.info' to be even more concise.