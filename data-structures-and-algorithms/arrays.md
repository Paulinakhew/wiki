# Arrays

## [Introduction to Data Structure: Arrays 101](https://leetcode.com/explore/featured/card/fun-with-arrays/521/introduction/) 

### Introduction

#### What is an Array?

* **array:** a collection of items that are stored in neighbouring \(contiguous\) memory locations
  * since the items are stored together, checking through the entire collection of items is straightforward

#### Creating an Array

```text
my_list = list()  # using the list() constructor  
another_list = [] # using square brackets 
```

#### Accessing Elements in Arrays

* **index:** a number that identifies each place in an array
* indexing is in the range of `0` to `n-1` where the first place is `0`, the second place is `1`, the third place is `2`, etc.

Example: print the second item of the list:

```text
thislist = ["apple", "banana", "cherry"]
print(thislist[1])  # prints banana
```

#### Writing Items into an Array with a Loop

Example: write the first 10 square numbers into a list

```text
new_list = []
for i in range(10):
    new_list[i] = (i + 1) * (i + 1)
```

#### Reading Items from an Array with a Loop

Example: print out everything that is in `new_list`

```text
for i in range(len(new_list)):
    print(new_list[i])
```

Example: a more elegant way of printing out the values of the array

```text
for num in new_list:
    print(num)
```

* we can use this when we don't need the index values
  * we can't use this when we are writing the squares into the array since we need the actual index numbers

