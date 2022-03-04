# #344: Reverse String

> Write a function that reverses a string. The input string is given as an array of characters s.

> You must do this by modifying the input array in-place with O(1) extra memory.

---

Yes, JS has built in methods to turn this into a one line code. Here it is:
` string.reverse()` <br />
Thats not my goal here. I want to understand the algorithms, so will not be using methods. Im going all natural; FKK, as the germans do.

##### In-place

To solve this problem, the array must be modified in-place. This means that there will be no new allocation in memory for a temporary array, retaining the O(1) notation for space complexity.
<br />

##### Technique

Will use the method of two pointers to modify the array in place.<br />
What does it mean? Well, you will use two pointers to point to the opposite sides of the array.
One will start by pointing to the left most element in the array, and the second will start by pointing to the very most right element in the array. **In other words, one points to the first element and one points to the last element of the array.**
With each iteration through the array, the left pointer and right pointer increase and decrease, respectivley, until finally they meet/collide in the middle.
Once they meet in the middle, it means every elemented was visited and the loop can end.

```JavaScript
    var reverseString = function(s) {
    let low = 0;
    let high = s.length -1;
        while(low < high){
            let temp = s[low];
            s[low] = s[high];
            s[high] = temp;
            low++;
            high--;
    }
};
```

##### Line by line solution

1. `let low = 0`:
   Set variable to 0. This will be the reference for the index of the elements in the first half of the arry.
2. `let high = s.length -1;`:
   Set variable to point to the length of the array. This will be used to point to elements in the second half of the array.
3. `while(left < right):`:
   Keep track of the left and right pointers. If they overlap, it means that the middle of the array has been reached and all elements have been sorted.
4. `let temp = s[low];`:
   Create new variable to temporarily store the value of element at `s[low]`.
5. `s[low] = s[high]`:
   The swap. Replace the value of the element at left location with the value of the variable at the right location.
6. `s[high] = temp;`
   The swap. Replace the value of the element at right location with temp (which was holding the value of the element at left location).
7. `low++`:
   Increment `low` by one to point to the next item in the array.
8. `high--`:
   Decrease `high` by one to point to the previous item in the array.
