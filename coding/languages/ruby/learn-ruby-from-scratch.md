# Learn Ruby from Scratch

These notes are taken from [this](https://www.educative.io/courses/learn-ruby-from-scratch) Educative online course, which I audited for free.

## Why should you learn Ruby?
### Programming is Creation
Motivate yourself to bring your code to life!
- when you run a program, a universe is created where things come to life and interact with each other
- as the creator, you define the rules
- e.g. creating an application like Twitter
    - create users
    - users can create tweets
    - users can follow each other
    - each time new users are created in your application, users have the ability to tweet and follow each other

## What are Variables?
This lesson gives an insight into variables and variable assignment.

### Naming Things
- variables: a way to assign names to objects that our program deals with

### Variable Assignment
- in Ruby, you can assign a name to an object by using the assignment operator `=`
```Ruby
puts number = 1
```

Output
```
1
```
- this assigns the name `number` to the object that is the number `1`
    - after, we can refer to this object by using the name `number`

```Ruby
number = 1
puts number
```

Output
```
1
```

### Variable is not a "thing"
- a variable is not an object by itself
    - it's just a _name_ for an object
- in the example, the number `1` is an object, while `number` is a name for it because we've assigned it

```Ruby
a = 1
puts a

large_number = 1
puts large_number

apples = 1
puts apples
```
Output:
```
1
1
1
```

- try and pick names that reveal your intention
- from the example, using `a`, `large_number`, and `apples` as names would be frowned upon because they aren't meaningful names and don't match the object
- a variable name is like a post-it note with the name `number` written on it and stuck on the object, the number `1`

## Reusing Variable Names
This lesson explains how variable names can be reused in Ruby
- a name is unique
    - the same name can only be assigned to one object at a time
- assigning different values to the same variable results in later assignments overwriting previous ones
- variable names can be re-used and re-assigned
```ruby
number = 4
number = number * 3
puts number + 2
```

Output
```
14
```
- continuing the post-it metaphor, this would stick a post-it with the name `number` on an object, and then later take it off and stick it on another object

### Explanation
- Ruby creates the number `4` on the __first line__ and assigns the name `number` to it
- on the __second line__, Ruby evaluates the expression `number * 3`, resulting in a new number `12` that is assigned to the `number` variable
- on the __third line__ Ruby adds `2` to the `number` object, resulting in `14`
- Ruby passes `14` to `puts`, which outputs it to the screen

- you can write the exact code with `puts 4 * 3 + 2`
- however, using variable names can be useful to break up long lines and make code more expressive and readable
- this is a __local variable__ and is the one that's used most often

## Things on the Right go First
This lesson describes how Ruby figures out the expression on the right first.

### Example
```ruby
number = 2 + 3 * 4
puts number
```
- Ruby needs to know what the object on the right is before it can assign the name `number` to it
- Ruby first evaluates the expression, which results in the number `14`
- Ruby then assigns the name `number` to the object
- the code temporarily looks like `number = 14` before the assignment `=` is evaluated

### Does this make sense?
- on the second line, Ruby passes the `number` variable (which is `14`) to `puts`, which outputs to the screen

## Types of Variables and their Usage
Get to know various kinds of variables in Ruby. Moreover, learn how and when to use them.

|   | Naming  | Scope  | Initialization  |
|---|---|---|---|
| Global Variables  | Global variables start with a `$` sign.  |  Their scope is global which means that they can be accessed from anywhere in a program. |  There’s no need to initilize. Uninitialized global variables have the value nil. |
|  Local Variables | Local variables begin with a lowercase letter or underscore(`_`).	  | The scope of a local variable ranges from class, module, def, or from a block’s opening brace to its close brace {}, i.e within its block of initialization.  |  No need to initialize. An uninitialized local variable is interpreted as methods with no arguments. |
| Instance Variables  |  They start with an `@` sign. | Their scope is limited to one instance of a class.  |   There’s no need to initilize. Uninitialized instance variables have the value nil. |
|  Class Variables |  Class variables start with an `@@` sign. |  Their scope is limited to the class in which they are created. |  They need to be initialized beforehand, otherwise they’ll result in error. |
