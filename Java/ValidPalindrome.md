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

To filter any character that is not an alphanumeric character, a helper function is necessary.

This helper function will validate the code of the character and determine whether it is alphanumeric or not. Depending on the answer, the function will return true or false.

If the function returns false, the pointer is told to 'ignore' the character and to move to the next character to get ready for comparison.

ex:
`string = 'abb.a'`

left and right hand pointer start at `string[0]` and `string[4]`, respectively.

Both the values are passed through the helper function which returns true, as they are valid characters.

A comparison is done to determine if the two values are the same. If so, the condition string is so far a palindrome and the pointers continue to traverse.

Next, left pointer moves to `string[1]` and right pointer moves to `string[3]`.

The value of the left pointer is a valid alphanumeric number, but the value of the right pointer is not and returns false.

Because the value is not an alphanumeric character, the right pointer ignores this character and moves to position `string[2]`.

It is then sent through the helper function to determine whether it is a valid alphanumeric character. Because it returns true, then the left pointer value `string[1]` and the right pointer value `string[2]` are compared.

The comparison returns true, meaning the string is a valid palindrome.
It returns true, meaning the string is a valid palindrome.

A very general overview of the process:

> What you see as a human "abb.a"

> What the function sees: "abba"

#### Code

```java
class Solution {
    public boolean isPalindrome(String s) {
        if(s.length() <= 1)
            return true;

        int left = 0;
        int right = s.length() -1;

        while(left < right){
            if(!isValid(s.codePointAt(left))){
                left++;
                continue;
            }
            if(!isValid(s.codePointAt(right))){
                right--;
                continue;
            }
            if(Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))){
                return false;
            }
            left++;
            right--;
        }
        return true;
    }

    public boolean isValid(int c){
        if((c >= 48 && c <= 57) || (c >= 65 && c <= 90) || (c >= 97 && c <= 122)){
            return true;
        }
        return false;
    }
}
```

###### Block by block explanation

- First looking at the helper function:

  - ```java
        public boolean isValid(int c){
            if((c >= 48 && c <= 57) || (c >= 65 && c <= 90) || (c >= 97 && c <= 122)){
                return true;
            }
            return false;
        }
    ```

    The character codes for numerical values are between 48 and 57.
    The character codes for lower case values are between 97 and 122.
    The character codes for upper case values are between 65 and 90.

    This function is determining whether the character value is equal to one of these alphanumeric conditions. If it is not, the function returns false.

- ```Java
    if(s.length() <= 1)
    return true;
  ```

  A catch case: if the word consists of one character, it is a palindrome by default. **ex: A**
  <br />

- ```java
  int left = 0;
  int right = s.length() -1;
  ```

  left and right are the two pointers that will traverse the string. Left starts at position 0 while right starts at the last position of the string.
  <br />

- ```Java
    while(left < right){
  ```
  The condition to control when the string traversing ends. This means, once left is no longer less than right, the two pointers have met in the middle and the all characters in the string have been looked at.
  <br />
- ```Java
    if(!isValid(s.codePointAt(left))){
        left++;
        continue;
    }
  ```

  Using the helperfunction `isValid()`, determine if the character is an alphanumeric character. Passed into the function is the `string.codePointAt(index)`. This is a built in function that converts the character to its unicode (numerical) value.

  This specific code block is working with the left hand pointer.
  If the function returns false, this means that it is not a letter or number and the value should be skipped over and the left side pointer will increase by one to visit the next value.

  The `continue` statement indicates to proceed to the next iteration of the while loop.
  <br />

- ```java
    if(!isValid(s.codePointAt(right))){
        right--;
        continue;
    }
  ```

  This is the same code logic as the previous if branch, excecpt this branch is specific to the right side pointer. If this branch determines that the character is not a letter or number, the pointer will decrease by one.

- ```java
    if(Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))){
        return false;
    }
  ```

  This is where the comparison happens.
  If the character that the left pointer points to is not the same representation of character that the right pointer points to, the string is not a palindrome and the function returns false.

  To make sure that cases are ignored, the lower case versions of the characters are compared.

- ```java
        left++;
        right--;

        }
        return true;
    }
  ```

  Finally, if the left and right character values were the same during the comparison, then it is necessary to compare the next values of the string. The left pointer is increased by one, and the right pointer is decreased by one.

  If by the time the pointers meet in the middle and all comparisons have been made, then the function returns true. This means that all comparisons were equal, nothing returned false, and the string is a valid palindrome.
