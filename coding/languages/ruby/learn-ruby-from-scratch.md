# Learn Ruby from Scratch

## Learn Ruby from Scratch

These notes are taken from [this](https://www.educative.io/courses/learn-ruby-from-scratch) Educative online course, which I audited for free.

## 1. Why should you learn Ruby?

### Programming is Creation

Motivate yourself to bring your code to life!

* when you run a program, a universe is created where things come to life and interact with each other
* as the creator, you define the rules
* e.g. creating an application like Twitter
  * create users
  * users can create tweets
  * users can follow each other
  * each time new users are created in your application, users have the ability to tweet and follow each other

## 2. Variables

### What are Variables?

This lesson gives an insight into variables and variable assignment.

#### Naming Things

* variables: a way to assign names to objects that our program deals with

#### Variable Assignment

* in Ruby, you can assign a name to an object by using the assignment operator `=`

  ```ruby
  puts number = 1
  ```

Output

```text
1
```

* this assigns the name `number` to the object that is the number `1`
  * after, we can refer to this object by using the name `number`

```ruby
number = 1
puts number
```

Output

```text
1
```

#### Variable is not a "thing"

* a variable is not an object by itself
  * it's just a _name_ for an object
* in the example, the number `1` is an object, while `number` is a name for it because we've assigned it

```ruby
a = 1
puts a

large_number = 1
puts large_number

apples = 1
puts apples
```

Output:

```text
1
1
1
```

* try and pick names that reveal your intention
* from the example, using `a`, `large_number`, and `apples` as names would be frowned upon because they aren't meaningful names and don't match the object
* a variable name is like a post-it note with the name `number` written on it and stuck on the object, the number `1`

### Reusing Variable Names

This lesson explains how variable names can be reused in Ruby

* a name is unique
  * the same name can only be assigned to one object at a time
* assigning different values to the same variable results in later assignments overwriting previous ones
* variable names can be re-used and re-assigned

  ```ruby
  number = 4
  number = number * 3
  puts number + 2
  ```

Output

```text
14
```

* continuing the post-it metaphor, this would stick a post-it with the name `number` on an object, and then later take it off and stick it on another object

#### Explanation

* Ruby creates the number `4` on the **first line** and assigns the name `number` to it
* on the **second line**, Ruby evaluates the expression `number * 3`, resulting in a new number `12` that is assigned to the `number` variable
* on the **third line** Ruby adds `2` to the `number` object, resulting in `14`
* Ruby passes `14` to `puts`, which outputs it to the screen
* you can write the exact code with `puts 4 * 3 + 2`
* however, using variable names can be useful to break up long lines and make code more expressive and readable
* this is a **local variable** and is the one that's used most often

### Things on the Right go First

This lesson describes how Ruby figures out the expression on the right first.

#### Example

```ruby
number = 2 + 3 * 4
puts number
```

* Ruby needs to know what the object on the right is before it can assign the name `number` to it
* Ruby first evaluates the expression, which results in the number `14`
* Ruby then assigns the name `number` to the object
* the code temporarily looks like `number = 14` before the assignment `=` is evaluated

#### Does this make sense?

* on the second line, Ruby passes the `number` variable \(which is `14`\) to `puts`, which outputs to the screen

### Types of Variables and their Usage

Get to know various kinds of variables in Ruby. Moreover, learn how and when to use them.

#### Definition and Usage

|  | Naming | Scope | Initialization |
| :--- | :--- | :--- | :--- |
| Global Variables | Global variables start with a `$` sign. | Their scope is global which means that they can be accessed from anywhere in a program. | There’s no need to initilize. Uninitialized global variables have the value nil. |
| Local Variables | Local variables begin with a lowercase letter or underscore\(`_`\). | The scope of a local variable ranges from class, module, def, or from a block’s opening brace to its close brace {}, i.e within its block of initialization. | No need to initialize. An uninitialized local variable is interpreted as methods with no arguments. |
| Instance Variables | They start with an `@` sign. | Their scope is limited to one instance of a class. | There’s no need to initilize. Uninitialized instance variables have the value nil. |
| Class Variables | Class variables start with an `@@` sign. | Their scope is limited to the class in which they are created. | They need to be initialized beforehand, otherwise they’ll result in error. |

#### Examples

**Global Variables**

```ruby
$global_var = "GLOBAL"  
non_global_var = "NON-GLOBAL"

def method1 
  puts "Global variable is #$global_var"   
end 

def method2 
  puts "Non-global variable is ", non_global_var    
end 

method1
method2
```

* `$global_var` is a global variable since it is preceded by a `$` sign
  * it can be accessed from anywhere in the program
* `non_global_var` is a simple variable
  * cannot be accessed from inside the `method2` so it gives an "undefined local variable or method" error

Output

```text
Global variable is GLOBAL

main.rb:9:in `method2': undefined local variable or method `non_global_var' for main:Object (NameError)
    from main.rb:13:in `<main>'
```

**Local Variables**

```ruby
var = "Hello World"
def foo 
  var = 1.5
  puts "Value of var in foo : ", var
end 

foo
puts "Value of var outside 'foo' method:", var
```

* there are two variables named `var` with different scopes
* the `var` inside the method has the local scope

Output

```text
Value of var in foo : 
1.5
Value of var outside 'foo' method:
Hello World
```

**Instance Variables**

```ruby
class Employee   
   def initialize(name)   
      @employee_name = name     
   end   

   def print()   
     puts "Employee name: #@employee_name"   
   end   
end   

# Create Objects   
e1 = Employee.new("Emma")   
e2 = Employee.new("David") 
e3 = Employee.new("Harris") 

# Call Methods   
e1.print()   
e2.print()   
e3.print()
```

* an instance variable starts with an `@` sign
* it belongs to only one instance of the class
* an uninitialized instance variable will have a `nil` value

Output

```text
Employee name: Emma
Employee name: David
Employee name: Harris
```

**Class Variables**

```ruby
class Employee   
   @@no_of_employees = 0   
   def initialize(name)   
      @employee_name = name   
      @@no_of_employees += 1   
   end   

   def total_no_of_employees()   
     puts "Total number of employees: #@@no_of_employees"   
   end   
end   

# Create Objects   
e1 = Employee.new("Emma")   
e2 = Employee.new("David") 
e3 = Employee.new("Harris") 

# Call Methods   
e1.total_no_of_employees()   
e2.total_no_of_employees()   
e3.total_no_of_employees()
```

* a class variable starts with a `@@` sign
* it should be initialized before use
* it belongs to the whole class and can be accessed from anywhere in the class
* a class variable is shared by all the descendants of the class
  * its value will change for every instance of the class

Output

```text
Total number of employees: 3
Total number of employees: 3
Total number of employees: 3
```

### Quick Quiz on Variables!

The quiz is located [here](https://www.educative.io/courses/learn-ruby-from-scratch/gx8NGOAZnqr).

## 3. Built-in Classes: Numbers

### Working with Numbers

This lesson goes through the types of number evaluations in Ruby.

#### 🔢 Numbers are Simply Numbers

* you can create a number by writing it e.g. `123` 
* **negative numbers** are created by prepending a minus `-`
* you can create **decimal numbers** by writing them e.g. `12.34`
* you can use an underscore `-` to separate thousands places e.g. `1_234.56` which is equal to `1234.56` 
* a number is defined by a series of digits, using a dot as a decimal mark, and optionally an underscore as a thousands separator

#### Kinds of Numbers

* there are different kinds of numbers
  * integer numbers aka "integers"
  * floating point numbers aka "floats"
* if you do a calculation with integer numbers you'll always get an integer back

```ruby
> 1 + 2
=> 3
```

* if there is a float, you'll get a float back

```ruby
> 1.0 + 2
=> 3.0
> 1 + 2.0
=> 3.0
```

* mathematical operations result in a floating point number except if all numbers used are integer numbers
* this is important when you do a division \(`/` means "divide by"\)

```ruby
> 3 / 2
=> 1
```

* decimal places will be cut off
  * use floating point \(decimal\) numbers when doing divisions

```ruby
> 3.0 / 2
=> 1.5
> 3 / 2.0
=> 1.5
```

#### Further Readings

* look through the [documentation for integer numbers](https://ruby-doc.org/core-2.2.2/Integer.html) 

### Exercise 1: Playing with Numbers

#### Problem Statement

In the exercise below, calculate:

* how many hours are in a year?
* how many minutes are in a decade?
* how to convert an age given in years seconds

#### Try it yourself

```ruby
def playing_with_numbers(hours_in_year, minutes_in_decade, age)
  hours_in_year = 24 * 365
  minutes_in_decade = 60 * hours_in_year * 10
  age_in_seconds = age * hours_in_year * 60 * 60


  return hours_in_year, minutes_in_decade, age_in_seconds 
end
```

3 of 3 Tests Passed

### Exercise 2: Guess the Type?

The quiz is located [here](https://www.educative.io/courses/learn-ruby-from-scratch/JP7jQlNG962).

### Exercise 3: Finding Modulo

#### Problem Statement

Find out what "modulo" means by asking Google and then calculate the modulo of two numbers given as an input.

#### Try it yourself

```ruby
def calculate_mod(num1, num2)
  result = num1 % num2
  
  return result
end
```

5 of 5 Tests Passed

### Exercise 4: Even or Odd?

Check whether a number is even or odd.

#### Problem Statement

Use a method from the [documentation](http://ruby-doc.org/core-2.2.2/Integer.html#method-i-odd-3F) to find out if given numbers are odd or even.

```ruby
def even_or_odd(num)
  result = num.even? ? "even" : "odd"
  
  return result
end
```

5 of 5 Tests Passed

## 4. Built-in Classes: Strings

### Working with Strings

This lesson will teach you how you can operate on strings in Ruby.

#### 🔤 A String, in programming languages, is text.

* a String is an object that represents a specific
* the most simple and common way to create Strings is to enclose some characters in quotes
  * you can use single or double qoutes

```ruby
"This is a string"
'This is another one'
```

#### Things you can do with Strings

* you can stick them together by using `+` 
  * this is called [concatenation](https://www.wikiwand.com/en/Concatenation)

```ruby
> "snow" + "ball"
=> "snowball"

> "hi" + "hi" + "hi"
=> "hihihi"
```

* you can replicate the last operation using `*` 

```text
> "hi" * 3
=> "hihihi"
```

* multiplying a String by a number in Ruby means repeating the String as many times

```text
> "1" + "1" + "1"
=> "111"

> "1" * 3
=> "111"
```

* Ruby behaves the same for Strings that contain nothing but numbers
* some other String methods:

```text
> "hello".upcase
=> "HELLO"

> "hello".capitalize
=> "Hello"

> "hello".length
=> 5

> "hello".reverse
=> "olleh"
```

* the last

