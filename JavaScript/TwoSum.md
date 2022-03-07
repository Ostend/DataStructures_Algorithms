# #1 Two Sum

> Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

> You may assume that each input would have exactly one solution, and you may not use the same element twice.

> You can return the answer in any order.

**Example:**

> **Input:** nums = [2,7,11,15], target = 9
> **Output:** [0,1] > **Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

---

# Code

###### Concepts:

- Hash map

### Two Versions

##### I. Nested loops, iterating through array: O(n^2)

```JavaScript
var twoSum = function(nums, target) {
    if(nums.length == 2){
        return([0, 1])
    }
    for(let i = 0; i<nums.length; i++){
        for(let j = 1; j<nums.length; j++){
            if(target - nums[i] == nums[j] && i != j){
                return([i,j])
            }
        }
    }
};
```

---

##### II. HashMap: O(n)

**The Hash map is an object that holds key value pairs.
Built in methods include**:

- `Map.get(key)`:
  Returns the value associated with the key.
- `Map.has(key)`:
  Returns boolean determining whether a key/value pair exists.
- `Map.set(key, value)`:
  Sets a new key value pair in the Map object.

**How will a HashMap work with this algorithm?** <br />
By iterating through the array and adding key/value pairs to the hashmap.

Let's, break it down further:

1. Start at the beginning of the array.
2. Subtract the `target` from `nums[i]` (`nums[0]` in this instance).
3. Look up in the hash map whether the difference exists. As this is the first iteration and the hash map is empty, the difference does not exist.
4. Add the new key/value pair to the hash map. Meaning: the key: `nums[i]` and the value `i` are added to the hash map. Key is the actual element and the value is the index where the element is located.
5. As the array is iterated through, the difference between target is calculated. The hash map is searched for said target key.
6. If the target is found, the function returns the **value** associated to the target **key**. Meaning the index location is returned.
7. If it is not found, the process repeats: a new key/value pair is added. Meaning the **key** is `nums[i]` and the **value** is `i`.
8. If no difference exists in the hash map by the time the loop is iterated through, no valid answer exists.

````javaScript
    var twoSum = function(nums, target) {
        let mapNums = new Map();
        for(let i = 0; i< nums.length; i++){
            if(mapNums.has(target - nums[i])){
                return([i, mapNums.get(target - nums[i])])
            }else{
                mapNums.set(nums[i], i)
            }
        }
    };
    ```
````
