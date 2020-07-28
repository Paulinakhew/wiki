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

#### Array Length

* **length:** the number of item inside the array
* to determine how many items a list has, use the `len()` function

Example: print the number of items in the list

```text
thislist = ["apple", "banana", "cherry"]
print(len(thislist))  # prints 3
```

#### Handling Array Parameters

* most array questions on LeetCode have an array passed in as a parameter



Here is a description for a problem you'll be asked to solve:

> Given a binary array, find the maximum number of consecutive 1s in this array.

* the only parameter is `nums`
* to iterate through all items in the array, we can do the following:

```text
class Solution:
    def findMaxConsecutiveOnes(self, nums: [int]) -> int:
        for i in range(len(nums)):
            pass
```



#### Problem: Max Consecutive Ones

Given a binary array, find the maximum number of consecutive 1s in this array.

Example 1:

```text
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```

Note:

* the input array will only contain `0` and `1`.
* the length of input array is a positive integer and will not exceed 10,000

```text
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        counts = []
        counter = 0
        for num in nums:
            if num == 1:
                counter += 1
            else:
                counts.append(counter)
                counter = 0
        counts.append(counter)
        return max(counts)
```



