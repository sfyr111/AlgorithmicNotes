# AlgorithmicNotes

## Array
[217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

Easy

This problem is about finding if any number shows up more than once in a list. We use a hashmap to keep track of each number. If we see a number that's already in the hashmap, it means there's a duplicate.

The time complexity is O(n), which means we go through the list just once. The space complexity is also O(n) because we need space to store each unique number in the hashmap.

```javascript
function containsDuplicate(nums) {
    let map = new Map();
    
    for (let i = 0; i < nums.length; i++) {
        if (map.has(nums[i])) {
            return true;
        }
        map.set(nums[i], true);
    }

    return false;
};
```

- **Key Concept**: Check for duplicates in a list.
- **Approach**: Use a hashmap to track each number's presence.
- **Key Phrases**:
    - "Finding if a number appears more than once"
    - "Using a hashmap for tracking"
    - "Time complexity is O(n), space complexity is O(n)"
- **Example Code Snippet**:
```javascript
if (map.has(nums[i])) return true;
map.set(nums[i], true);
```

[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

Easy

To check if two strings are anagrams(meaning they are made of the same characters in a different order), we can use two hashmaps to record the occurrence count of each character in both strings. After that, we compare the two hashmaps to see if they are identical. 

The time complexity of O(n) and the space complexity of O(n). Iterates through each character of both strings once and uses two hashmaps to store their character count.


```javascript
function isAnagram(s, t) {
    if (s.length !== t.length) {
        return false;
    }

    const countA = {};
    const countB = {};

    for (let i = 0; i < s.length; i++) {
        countA[s[i]] = 1 + (countA[s[i]] || 0);
        countB[t[i]] = 1 + (countB[t[i]] || 0);
    }

    const entriesA = Object.entries(countA);
    // const entriesB = Object.entries(countB);

    for (const [key, value] of entriesA) {
        if (countB[key] !== value) {
            return false;
        }
    }

    return true;
};
```

- **Key Concept**: Check if two strings have the same characters in different orders.
- **Approach**: Use two hashmaps to track the count of each character in both strings, then compare these counts.
- **Key Phrases**:
    - "Determining if strings are anagrams with hashmaps"
    - "Counting character occurrences in each string"
    - "Equal character counts indicate anagrams"
- **Example Code Snippet**:
```javascript
countA[s[i]] = (countA[s[i]] || 0) + 1;
if (countB[key] !== value) return false;
```

[1. Two Sum](https://leetcode.com/problems/two-sum/)

Easy

We use a hashmap to store each number along with its index, where the number is the key and the index is the value. We iterate through the array to find the difference between the target and the current number. If this difference is already in the hashmap, it means we have found a pair that adds up to the target, and we return their indices.

The time complexity is O(n) because we only need to go through the array once. The space complexity is also O(n) as we create a hashmap to store each number and its index.

```javascript
var twoSum = function(nums, target) {
    let obj = {};

    for (let i = 0; i < nums.length; i++) {
        const diff = target - nums[i];
        
        if (obj[diff] !== undefined) {
            return [i, obj[diff]];
        }

        obj[nums[i]] = i;
    }

    return [];
    
};
```

- **Key Concept**: Find two numbers that add up to a specific target.
- **Approach**: Store each number and its index in a hashmap, checking for the complement of each number.
- **Key Phrases**:
    - "Using a hashmap to store numbers and indices"
    - "Finding two numbers that sum up to the target"
    - "Iterate once, time and space complexity O(n)"
- **Example Code Snippet**:
```javascript
const diff = target - nums[i];
if (obj[diff] !== undefined) return [i, obj[diff]];
