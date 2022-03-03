# #344: Reverse String

> Write a function that reverses a string. The input string is given as an array of characters s.

> You must do this by modifying the input array in-place with O(1) extra memory.

---

##### In-place

To solve this problem, the array must be modified in-place. This means that there will be no new allocation in memory for a temporary array, retaining the O(1) notation for space complexity.
<br />

##### Technique

Will use the method of two pointers to modify the array in place.

```java
public void reverseString(char[] s){
    int left = 0;
    int right = s.length -1;
    while(left < right){
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;
        left++;
        right--;
    }
}
```

Line by line solution:

1. `int left = 0;`:
   `left` represents the integer value for the index of the first element in the array.
2. `int right = s.length - 1;`:
   `right ` represents the integer value for the index of the last element of the array.
3. `while(left < right)`:
   When the index value pointing to the first half of the array meets with the index value of the right half of the array, it indicates that all elements of the array have been accessed and to end the loop.
4. `char temp = s[left];`:
   Create a temporary char element to store the value at index `s[left]`.
5. `s[left] = s[right];`:
   The value at index `s[right]` is swapped for the value at index location `s[left]`.
6. `s[right] = temp;`:
   The value for element at index `s[right]` is replaced with `temp` (which holds the value `s[left`])
7. `left ++;`:
   Incremint value of left by one to proceed to next element in the array, eventually making its way to the middle of the array where it will meet with `right`.
8. `right --;`:
   Decrease value of right by one to proceed to preceeding element in the array, eventually making its way to the middle of the array where it will meet iwth `left`.
