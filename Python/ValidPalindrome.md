# #125 Valid Palindrome

> A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

> Given a string s, return true if it is a palindrome, or false otherwise.

==Example 1==

> Input: s = "A man, a plan, a canal: Panama"
> Output: true
> Explanation: "amanaplanacanalpanama" is a palindrome.

---

#### Technique

First, its important to get a grasp of the question.
Not only does it ask to **return a valid palindrome**, but it asks:

- Ignore white spaces.
- Ignore any other characters that are not capital/lowercase letters or numbers.

**With that in mind, how is it possible to tell if a string is a palindrome?**

If a string reads the same forward and backwards, that means we can use the two pointer method.

One pointer begins at the first character of the string. The second pointer begins at the last character of the string.

If both the first and last characters of the string are the same, so far so good! A palindrome is possible. Then each pointer can be shifted to represent the next character and the comparison can be made again.

If the characters of the two pointers are not the same, then our string is not a palindrome.

Ex:
`string = "abba" `
left pointer points to 'a' and right pointer points to 'a', `string[0]` and `string[3]` respectively.

Because both characters that the pointer points to are equal, the pointers will continue to traverse the string.

Left pointer increases by one to point to 'b', and right pointer decreases by one to point to 'b', `string[1]` and `string[2]`, respectively.

Because all cases found that the comparisons of characters were equal, then it is a valid palindrome.

**What about the special characters**

To filter any character that is not an alphanumeric character, python3 has a built in function `String.isalnum()` which will return true if the character is alphanumeric.

An if branch will validate the code of the character and determine whether it is alphanumeric or not. Depending on the answer, the function will return true or false.

If `String.isalnum()` returns false, the pointer is told to 'ignore' the character and to move to the next character to get ready for comparison.

ex:
`string = 'abb.a'`

left and right hand pointer start at `string[0]` and `string[4]`, respectively.

Both the values are passed through the `String.isalnum()` method which returns true, as they are valid characters.

A comparison is done to determine if the two values are the same. If so, the condition string is so far a palindrome and the pointers continue to traverse.

Left pointer moves to `string[1]` and right pointer moves to `string[3]`.

The value of the left pointer is a valid alphanumeric number, but the value of the right pointer is not and returns false.

Because the value is not an alphanumeric character, the right pointer ignores this character and moves to position `string[2]`.

`string[2].isalnum()` determines whether it is a valid alphanumeric character. Because it returns true, then the left pointer value `string[1]` and the right pointer value `string[2]` are compared.

The comparison returns true, meaning the string is a valid palindrome.

A very general overview of the process:

> What you see as a human "abb.a"

> What the function sees: "abba"

#### Code

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        if(len(s) <= 1):
            return True
        left, right = 0, len(s) - 1

        while(left < right):
            if not s[left].isalnum():
                left+=1
            elif not s[right].isalnum():
                right-=1
            elif(s[left].lower() != s[right].lower()):
                return False
            else:
                left+=1
                right-=1
        return True


```

###### Block by block explanation

- ```python
    if(len(s) <= 1):
        return True
  ```

  A catch case: if the word consists of one character, it is a palindrome by default. **ex: A**
  <br />

- ```python
     left, right = 0, len(s) - 1
  ```

  left and right are the two pointers that will traverse the string. Left starts at position 0 while right starts at the last position of the string.
  <br />

- ```python
    while(left < right):
  ```
  The condition to control when the string traversing ends. This means, once left is no longer less than right, the two pointers have met in the middle and the all characters in the string have been looked at.
  <br />
- ```python
    if not s[left].isalnum():
            left+=1
    elif not s[right].isalnum():
            right-=1
  ```

  Using the method `String.isalnum()` to determine if the character is an alphanumeric character.

  The first branch looks at the left pointer. If the value is not alphanumeric, the left poitner proceeds to the next position in the string.

  The second branch looks at the right pointer. If the value is not aplhanumeric, the right pointer decreases to the next position in the string.
  <br />

- ```python
    elif(s[left].lower() != s[right].lower()):
        return False
  ```

  This is where the comparison happens.
  If the character that the left pointer points to is not the same representation of character that the right pointer points to, the string is not a palindrome and the function returns false.

  To make sure that cases are ignored, the lower case versions of the characters are compared.

- ```python
        else:
            left+=1
            right-=1
    return True
  ```

  Finally, if the left and right character values were the same during the comparison, then it is necessary to compare the next values of the string. The left pointer is increased by one, and the right pointer is decreased by one.

  If by the time the pointers meet in the middle and all comparisons have been made, then the function returns true. This means that all comparisons were equal, nothing returned false, and the string is a valid palindrome.
