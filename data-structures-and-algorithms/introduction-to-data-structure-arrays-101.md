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

```text
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        return sorted(x*x for x in A)
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

![Inserting an element at the end of an array.](../.gitbook/assets/image%20%288%29.png)

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

![Inserting an element at the front of the array.](../.gitbook/assets/image%20%287%29.png)

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

![Inserting an element at a specific index.](../.gitbook/assets/image%20%289%29.png)

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

## Deleting Items From an Array

### Array Deletions

* deleting in an array has the same three different cases:
  * deleting the last element
  * deleting the first element
  * deleting at any given index

#### Deleting From the End of an Array

* the least time consuming of the three cases

![Deleting an element from the end of the array.](../.gitbook/assets/image%20%2810%29.png)

* to remove an item from the end of the list, use the `pop()` method

```text
thislist = ["apple", "banana", "cherry"]
thislist.pop()
print(thislist)  # outputs ["apple", "banana"]
```

#### Deleting From the Start of an Array

* deleting from the front of the array is the costliest operation
  * it will create a vacant spot at the `0th` index and all of the other elements will have to shift one element to the left
* shifting all elements will take **O\(n\)** time, where **n** is the number of elements in the array

![Deleting an element from the start of an array.](../.gitbook/assets/image%20%286%29.png)

* to remove an element from the front of the list, use the `pop()` method and pass in `0` as the index

```text
thislist = ["apple", "banana", "cherry"]
thislist.pop(0)
print(thislist)  # outputs ["banana", "cherry"]
```

* alternatively, you can use the `del` keyword to remove the specified index

```text
thislist = ["apple", "banana", "cherry"]
del thislist[0]
print(thislist)  # outputs ["banana", "cherry"]
```

#### Deleting From Anywhere in the Array

* to delete at any given index, the empty space created by the deleted item will have to be filled
  * each of the elements to the right of the index we are deleting at will get shifted to the left by 1
* deleting the first element of an array is a special case of deletion at a given index, where the index is `0`
* the shift of elements takes **O\(k\)** time where **k** is the number of elements to the right of the given index
  * since potentially _**k = n**_, we say the time complexity of this operation is also **O\(n\)**

![Deleting an element from any index in the array.](../.gitbook/assets/image%20%285%29.png)

Example: deleting the second element in the array using the `pop()` method

```text
thislist = ["apple", "banana", "cherry"]
thislist.pop(1)
print(thislist)  # outputs ["apple", "cherry"]
```

### Problem: Remove Element

Given an array _nums_ and a value _val_, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example 1:**

```text
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```text
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.

Note that the order of those five elements can be arbitrary.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```text
// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

```text
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        while val in nums:
            nums.pop(nums.index(val))
```



### Problem: Remove Duplicates from Sorted Array

Given a sorted array _nums_, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only _once_ and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

**Example 1:**

```text
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```text
Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```text
// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

```text
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 0
        while i < len(nums) - 1:
            while nums[i+1] == nums[i]:
                nums.pop(nums.index(nums[i]))
            i += 1
```

## Search in an Array

* searching is the most important operation
* the speed of searching for an element in a data structure helps programmers make design choices for their codebases
* there are multiple ways to search an array
* **searching** means to find an occurrence of a particular element in the array and return its position
  * might need to search an array to find out whether or not an element is present in an array
  * might want to search an array to find which index to insert a new element at
* if we know the index in the array that might have the element we are looking for, the search becomes a constant time operation, **O\(1\)**
  * we go to the given index and check whether or not the element is there

### Linear Search

* if the index is not known, we can check every element in the array
  * we continue checking elements until we find the element we're looking for or we reach the end of the array
* **linear search algorithm:** technique for finding an element by checking through all elements one by one
  * in the worst case, a linear search checks the entire array
  * the time complexity for a linear search is **O\(n\)**

Example: the linear search algorithm in action, with all the edge cases handled properly.

```text
def linear_search(my_list, val):
    # Check for edge cases. Is the array null or empty?
    # if it is, the we return false because the element we're
    # searching for couldn't possibly be in it
    if not my_list:
        return False
    
    # Carry out the linear search by checking each element,
    # starting from the first one.
    for i in range(len(my_list)):
        if my_list[i] == val:
            return True
    
    # We didn't find the element in the array.
    return False
```

* this is the function we can call to see whether or not an element is in an array
* we take care of the edge cases before proceeding with the actual search
  * we don't check the rest of the elements once we found the element we were looking for

### Binary Search

* if the elements in the array are in sorted order, we can use binary search
* **binary search:** where we repeatedly look at the middle element in the array and determine whether the element we are looking for is to the left or to the right
  * each time we do this, we halve the number of elements we need to search, making binary search a lot faster than linear search
* only works if the data is sorted
* if we are doing a single search, it is faster to do a linear search
  * it takes longer to sort than to linear search
* if we are performing a lot of searches, it is worth sorting the data first so we can use binary search for repeated searches

### Problem: Check if N and Its Double Exist

Given an array `arr` of integers, check if there exists two integers `N` and `M` such that `N` is the double of `M` \( i.e. `N = 2 * M`\).

More formally check if there exists two indices `i` and `j` such that :

* `i != j`
* `0 <= i, j < arr.length`
* `arr[i] == 2 * arr[j]`

**Example 1:**

```text
Input: arr = [10,2,5,3]
Output: true
Explanation: N = 10 is the double of M = 5,that is, 10 = 2 * 5.
```

**Example 2:**

```text
Input: arr = [7,1,14,11]
Output: true
Explanation: N = 14 is the double of M = 7,that is, 14 = 2 * 7.
```

**Example 3:**

```text
Input: arr = [3,1,7,11]
Output: false
Explanation: In this case does not exist N and M, such that N = 2 * M.
```

**Constraints:**

* `2 <= arr.length <= 500`
* `-10^3 <= arr[i] <= 10^3`

```text
class Solution:
    def checkIfExist(self, arr: List[int]) -> bool:
        for i in range(len(arr)):
            # check if double exists in all other elements
            if arr[i] * 2 in (arr[:i] + arr[i+1:]):
                return True
            # check if half exists in all other elements if number is even
            elif arr[i] % 2 == 0:
                if arr[i] / 2 in (arr[:i] + arr[i+1:]):
                    return True
        return False
```

### 

### Problem: Valid Mountain Array

Given an array `A` of integers, return `true` if and only if it is a _valid mountain array_.

Recall that A is a mountain array if and only if:

* `A.length >= 3`
* There exists some `i` with `0 < i < A.length - 1` such that:
  * `A[0] < A[1] < ... A[i-1] < A[i]`
  * `A[i] > A[i+1] > ... > A[A.length - 1]`

![](https://assets.leetcode.com/uploads/2019/10/20/hint_valid_mountain_array.png)

**Example 1:**

```text
Input: [2,1]
Output: false
```

**Example 2:**

```text
Input: [3,5,5]
Output: false
```

**Example 3:**

```text
Input: [0,3,2,1]
Output: true
```

**Note:**

1. `0 <= A.length <= 10000`
2. `0 <= A[i] <= 10000` 

```text
class Solution:
    def validMountainArray(self, A: List[int]) -> bool:
        if len(A) < 3:
            return False
        dec = False

        # check that the array starts by increasing
        if A[0] > A[1]:
            return False

        for i in range(len(A) - 1):
            # not strictly increasing
            if A[i] == A[i+1]:
                return False
            # initialize inc bool to be True
            elif A[i] < A[i+1] and dec:
                return False
            # if the array starts decreasing
            elif A[i] > A[i+1]:
                dec = True
            # if the array has already decreased, it shouldn't increase again
            elif dec and A[i] < A[i+1]:
                return False

        if not dec:
            return False
        return True
```

```text
class Solution:
    def validMountainArray(self, A: List[int]) -> bool:
        n = len(A)
        i = 0
        
        #walk up
        while i+1 < n and A[i] < A[i+1]:
            i += 1
            
        # peak can't be first or last
        if i == 0 or i == n-1:
            return False
            
        # walk down
        while i+1 < n and A[i] > A[i+1]:
            i += 1
        
        return i == n-1
```



