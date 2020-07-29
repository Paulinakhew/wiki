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

![Inserting an element at the end of an array.](../.gitbook/assets/image%20%286%29.png)

* we can add an item to the end of the list using the `append()` method

Example: using the `append()` method to append an item

```text
thislist = ["apple", "banana", "cherry"]
thislist.append("orange")
print(thislist)  # outputs ["apple", "banana", "cherry", "orange"]
```

#### Inserting at the Start of an Array

* to insert an element at the start of an array, we'll need to shift the other elements in the array to the right by 1 to make space for the new element
* the time taken for insertion at the beginning of the array is proportional to the length of the array
  * this is linear time complexity: **O\(n\)**

![Inserting an element at the front of the array.](../.gitbook/assets/image%20%285%29.png)

* to add an item at a specified index, use the `insert()` method
  * to add it to the front of the list, insert at position 0

Example: using `insert()` to insert at the front of the list

```text
thislist = ["apple", "banana", "cherry"]
thislist.insert(0, "orange")
print(thislist)  # outputs ["orange", "apple", "banana", "cherry"]
```

#### Inserting Anywhere in the Array

* to insert at any given index, we first need to shift all the elements past that index one position to the right
* once the space is created, we insert the new element
  * inserting at the beginning is a special case of inserting an element at a given index - the given index is `0`

![Inserting an element at a specific index.](../.gitbook/assets/image%20%287%29.png)

* this is a costly operation since we could _potentially_ have to shift all of the elements to the right before inserting the new element
* to add an item at a specified index, use the `insert()` method

```text
thislist = ["apple", "banana", "cherry"]
thislist.insert(1, "orange")
print(thislist)  # outputs ["apple", "orange", "banana", "cherry"] 
```



### Problem: Duplicate Zeros

Given a fixed length array `arr` of integers, duplicate each occurrence of zero, shifting the remaining elements to the right.

Note that elements beyond the length of the original array are not written.

Do the above modifications to the input array **in place**, do not return anything from your function.

**Example 1:**

```text
Input: [1,0,2,3,0,4,5,0]
Output: null
Explanation: After calling your function, the input array is modified to: [1,0,0,2,3,0,0,4]
```

**Example 2:**

```text
Input: [1,2,3]
Output: null
Explanation: After calling your function, the input array is modified to: [1,2,3]
```

**Note:**

1. `1 <= arr.length <= 10000`
2. `0 <= arr[i] <= 9`

```text
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        """
        Do not return anything, modify arr in-place instead.
        """
        new_arr = []
        for num in arr:
            if num != 0:
                new_arr.append(num)
            else:
                new_arr.append(0)
                new_arr.append(0)
        for i in range(len(arr)):
            arr[i] = new_arr[i]
```

### 

### Problem: Merge Sorted Array

Given two sorted integer arrays _nums1_ and _nums2_, merge _nums2_ into _nums1_ as one sorted array.

**Note:**

* The number of elements initialized in _nums1_ and _nums2_ are _m_ and _n_ respectively.
* You may assume that _nums1_ has enough space \(size that is **equal** to _m_ + _n_\) to hold additional elements from _nums2_.

**Example:**

```text
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

**Constraints:**

* `-10^9 <= nums1[i], nums2[i] <= 10^9`
* `nums1.length == m + n`
* `nums2.length == n`

```text
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        sort = []
        i = 0
        j = 0
        while i < m and j < n:
            if nums1[i] <= nums2[j]:
                sort.append(nums1[i])
                i += 1
            else:
                sort.append(nums2[j])
                j += 1
        if i < m:
            while i < m:
                sort.append(nums1[i])
                i += 1
        if j < n:
            while j < n:
                sort.append(nums2[j])
                j += 1
        for i in range(len(nums1)):
            nums1[i] = sort[i]
```

```text
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        nums1[m:] = nums2
        nums1.sort()
```



