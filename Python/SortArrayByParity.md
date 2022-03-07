# #905 Sort Array by Parity

> Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

> Return any array that satisfies this condition.

**Example 1**

> Input: nums = [3,1,2,4]
> Output: [2,4,3,1]

> Explanation: The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.

#### Technique

Okay, what is the question asking. Lets be broad.

1. Find the even numbers
2. Find the odd numbers.

Lets take it one step further, what does leetcode want?

3. Put the even numbers in the front of the array.
4. Put the odd numbers in the back of the array.

There we go, very simple and very clear.

**What’s the catch case?**
If the array length is 1 or less, go ahead and return it back. It is already, by default, sorted.

**The method**
Two pointers and swapping.

- Left pointer points to the beginning of the array.
- Right pointer points to the end of the array.

The pointers traverse the array, shifting closer together inward, UNTIL they overlap. If this happens, it means that all the numbers have been looked at and to end the iteration.

**How to detect for even/odd numbers**
Using the modulo operator : `%`

The modulo operator returns the remainder of the left hand value divided by the right hand value. Ex: `1 % 1 = 0` reads: `1/1 = 1, no remainder`.

Using this logic:

1. Any even number that is divided by two will not have a remainder.
2. Using the %: `if number % 2 == 0` then the number is even. Else, it is odd.

**POINTERS, SWAPPING, AND MODULO MEET**
To implement all of the above together:

1. Left pointer points to the first element in the array.
2. Right pointer points the last element in the array.
3. The value that left pointer is pointing to is tested whether it is even using the modulo operator.
   1. If it is even, increase the left pointer by one to visit the next value in the array.
   2. If it is odd: swap the odd value that the pointer is pointing to with the value of the right side of the array that the right pointer is pointing to. **Then decrease the right pointer by one**. As you know for certain that number is odd, you do not need to visit it again and can safely step down to the next array element.
4. Iterate through the array until all left and right elements have been analysed. Then return the sorted array.

#### Code

```python
class Solution:
    def sortArrayByParity(self, nums: List[int]) -> List[int]:
        if len(nums) <= 1:
            return nums
        left = 0
        right = len(nums) -1
        while(left < right):
            if(nums[left] % 2 == 0):
                left+=1
            else:
                temp = nums[left]
                nums[left] = nums[right]
                nums[right] = temp
                right-=1
                continue
        return nums
```

###### Block by block explanation

- ```python
    if len(nums) <= 1:
            return nums
  ```
  The catch case: if the length is one number or less, return immediatley.
- ```python
        left = 0
        right = len(nums) -1
  ```
  The left and right pointers. Left points to the first element in the array. Right points to the last element of the array.
- ```python
    while(left < right):
  ```
  The condition that while the left pointer is less than the right pointer, continue. If not, it means that the pointers have crossed paths and the iteration will end. Remember that the pointers represent the index value of an element in the array.
- ```python
    if(nums[left] % 2 == 0):
        left+=1
  ```

  **Modulo** operator in use. This is the meat of the algorithm. To dethermin if the number that the left pointer is pointing to is even or odd. If it is, the pointer increases by one to point to the next element in the array.

- ```python
    else:
        temp = nums[left]
        nums[left] = nums[right]
        nums[right] = temp
        right-=1
        continue
  ```
  **SWAPPING** The other meat of the algorithm. If the number is odd, then it needs to be added to the end of the list. To do this, swap odd number that the left pointer is pointing to with the number that the right pointer is pointing to.
  Then, decrease the right pointer by one, as it is an odd number and to proceed to the next element in the array.
- ```python
    return nums
  ```
  Once all of the numbers have been visited and the array has been sorted, return the array.
