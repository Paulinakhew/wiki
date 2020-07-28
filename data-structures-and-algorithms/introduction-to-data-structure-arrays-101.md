# Arrays

{% embed url="https://leetcode.com/explore/learn/card/fun-with-arrays/" caption="This LeetCode Explore Card will help you understand the basics of Arrays." %}

## [Introduction](https://leetcode.com/explore/featured/card/fun-with-arrays/521/introduction/)

### What is an Array?

* **array:** a collection of items that are stored in neighbouring \(contiguous\) memory locations
  * since the items are stored together, checking through the entire collection of items is straightforward

### Python Collections \(Arrays\)

* there are four collection data types in the Python programming language:
  * **list**: a collection which is ordered and changeable
    * allows duplicate members
  * **tuple:** a collection which is ordered and unchangeable
    * allows duplicate members
  * **set:** a collection which is unordered and unindexed
    * no duplicate members
  * **dictionary:** a collection which is unordered, changeable, and indexed
    * no duplicate members

#### Creating an Array

> Note: I will be using a Python List for this page.

```text
my_list = list()  # using the list() constructor  
another_list = [] # using square brackets 
```

### Accessing Elements in Arrays

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

### Array Length

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



### Problem: Max Consecutive Ones

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



### Problem: Find Numbers with Even Number of Digits

Given an array `nums` of integers, return how many of them contain an **even number** of digits.



**Example 1:**

```text
Input: nums = [12,345,2,6,7896]
Output: 2
Explanation: 
12 contains 2 digits (even number of digits). 
345 contains 3 digits (odd number of digits). 
2 contains 1 digit (odd number of digits). 
6 contains 1 digit (odd number of digits). 
7896 contains 4 digits (even number of digits). 
Therefore only 12 and 7896 contain an even number of digits.
```

**Example 2:**

```text
Input: nums = [555,901,482,1771]
Output: 1 
Explanation: 
Only 1771 contains an even number of digits.
```

**Constraints:**

* `1 <= nums.length <= 500`
* `1 <= nums[i] <= 10^5`

```text
class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        count = 0
        for number in nums:
            if len(str(number)) % 2 == 0:
                count += 1
        return count
```



### Problem: Squares of a Sorted Array

Given an array of integers `A` sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.  
**Example 1:**

```text
Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
```

**Example 2:**

```text
Input: [-7,-3,2,3,11]
Output: [4,9,9,49,121]
```

**Note:**

1. `1 <= A.length <= 10000`
2. `-10000 <= A[i] <= 10000`
3. `A` is sorted in non-decreasing order.

```text
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        final = []
        for number in A:
            final.append(number * number)
        return sorted(final)
```



## [Inserting Items Into an Array](https://leetcode.com/explore/learn/card/fun-with-arrays/525/inserting-items-into-an-array/3243/)

### Basic Array Operations

* arrays support the following operations:
  * insert
  * delete
  * search

### Array Insertions

* inserting a new element into an array can take many forms:
  * inserting at the end
  * inserting at the beginning
  * inserting at any given index

#### Inserting at the End of the Array

* we can add an item to the end of the list using the `append()` method

Example: using the `append()` method to append an item

```text
thislist = ["apple", "banana", "cherry"]
thislist.append("orange")
print(thislist)  # outputs ["apple", "banana", "cherry", "orange"]
```

