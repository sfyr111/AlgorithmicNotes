
# Table of Contents
- [Array](#Array)
  - [217. Contains Duplicate](#217-contains-duplicate)
  - [242. Valid Anagram](#242-valid-anagram)
  - [1. Two Sum](#1-two-sum)
  - [49. Group Anagrams](#49-group-anagrams)
  - [347. Top K Frequent Elements](#347-top-k-frequent-elements)
  - [238. Product of Array Except Self](#238-product-of-array-except-self)
  - [36. Valid Sudoku](#36-valid-sudoku)
  - [128. Longest Consecutive Sequence](#128-longest-consecutive-sequence)


## Array

### [217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

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

### [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)

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

### [1. Two Sum](https://leetcode.com/problems/two-sum/)

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
```

### [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)

Medium

To group anagrams, we use a hashmap where the key is a unique identifier generated from the frequency of each letter in a string. We achieve this by using a fixed-size array of 26 elements to represent the frequency of each letter (assuming lowercase English letters). Each position in the array corresponds to a letter, and we increment the count as we encounter each letter in the strings.

```javascript
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function(strs) {
    let obj = {};
    
    for (let i = 0; i < strs.length; i++) {
        const count = new Array(26).fill(0);
        for (let s of strs[i]) {
            count[s.charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
        }
        const key = count.join('#');

        if (!obj[key]) {   
            obj[key] = [];
        }
        obj[key].push(strs[i])

    }

    return Object.values(obj);
};
```

- **Key Concept**: Grouping strings that are anagrams into the same category.
- **Approach**: Use a hashmap with keys generated from each string's character frequency.
- **Key Phrases**:
    - "Grouping anagrams using a hashmap."
    - "Unique key from letter frequencies."
    - "Fixed-size array for character count."
    - "each position in the array corresponds to a letter"
    - "each position be a number representing the frequency of the letter"
    - "Time complexity is O(n), space complexity is O(n)."
- **Example Code Snippet**:
```javascript
const count = new Array(26).fill(0); // Frequency array for each letter
count[s.charCodeAt(0) - 'a'.charCodeAt(0)]++; // Increment letter count
const key = count.join('#'); // Generate unique key for the hashmap
obj[key] = (obj[key] || []).concat(strs[i]); // Group anagrams together
```

### [347. Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

Medium

To identify the top k frequent elements, we first utilize a hashmap, with each element as a key and its frequency as the value. Next, we convert this information into an array, where each index represents a frequency, and we place the elements into positions that match their frequencies. Finally, by iterating through the array from the highest frequencies to the lowest, we extract the top k frequent numbers.

```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var topKFrequent = function(nums, k) {
    const frequentMap = new Map();
    const counts = new Array(nums.length + 1).fill().map(() => [])
    
    for (let i = 0; i < nums.length; i++) {
        frequentMap.set(nums[i], (frequentMap.get(nums[i]) || 0) + 1);
    }

    for (let [num, frequent] of frequentMap) {
        counts[frequent].push(num);
    }    

    let res = [];

    for (let j = counts.length - 1; j >= 0; j--) {
        if (counts[j].length > 0) {
            if (k === 0) break;
            for (let c of counts[j]) {
                k -= 1;
                res.push(c);
            }
        }
    }

    return res;
};
```

- **Key Concept**: Record frequencies with a map and then find the top k by converting to an array.
- **Approach**: Count element frequencies using a hashmap, sort or iterate these frequencies, and then select the top k elements.
- **Key Phrases**:
    - "Using a hashmap to track element frequencies."
    - "Converting frequency data into an array."
    - "Array indices represent frequencies."
    - "Iterating from array find the top k number"
- **Example Code Snippet**:
```javascript
// Record each element's frequency in a hashmap
frequentMap.set(nums[i], (frequentMap.get(nums[i]) || 0) + 1);

// Convert frequencies into an array index, storing elements at these indices
counts[frequent].push(num);

// Retrieve the top k frequent elements by traversing the array from the end
for (let c of counts[j]) {
    if (k === 0) break;
    res.push(c);
    k--;
}

```

### [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

Medium
  
To solve the problem efficiently, we recognize that the product at each position in the array can be derived from multiplying all the elements to the left of that position by all the elements to the right. This insight allows us to avoid the brute force approach, which would involve nested loops and result in O(n^2) time complexity. Instead, we calculate the products of all elements to the left and to the right of every position, then multiply these two values to get the result for each position, ensuring O(n) time complexity. It's important to note that the first element of the prefix product and the last element of the suffix product should be 1, as there are no elements outside their respective sides.

To solve the problem efficiently, we can calculate the products of all elements to the left and right of every position, then multiply them. This way, we avoid nested loops and get O(n) time complexity. Remember that the first element of the prefix product and the last element of the suffix product are always 1.

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
    const n = nums.length;
    const prefix = new Array(n);
    const suffix = new Array(n);
    const result = new Array(n);

    prefix[0] = 1;
    for (let i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] * nums[i - 1];
    }

    suffix[n - 1] = 1;
    for (let j = n - 2; j >= 0; j--) {
        suffix[j] = suffix[j + 1] * nums[j + 1];
    }

    let m = 0;
    while (m < n) {
        result[m] = prefix[m] * suffix[m];
        m++;
    }
    
    return result;
};
```

- **Key Concept**: Calculate the result for each position by multiplying the left and right products.
- **Approach**: Use two arrays to hold the products of all elements to the left and right of each position, then multiply these for the final result.
- **Key Phrases**:
    - "Avoiding brute force and nested loops."

    - "Prefix and suffix product arrays."
    - "First and last elements of product arrays are 1."
    - "Linear time complexity O(n)."
- **Example Code Snippet**:
```javascript
// Initialize prefix and suffix products
prefix[0] = 1;
suffix[n - 1] = 1;

// Compute prefix products
for (let i = 1; i < n; i++) {
    prefix[i] = prefix[i - 1] * nums[i - 1];
}

// Compute suffix products
for (let j = n - 2; j >= 0; j--) {
    suffix[j] = suffix[j + 1] * nums[j + 1];
}

// Multiply prefix and suffix products for the result
for (let m = 0; m < n; m++) {
    result[m] = prefix[m] * suffix[m];
}
```

### [36. Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)

Medium

We use three hash tables to keep track of all the numbers in each row, column, and 3x3 square of the Sudoku board. The key part is figuring out the index for each square, which we do with `3 * Math.floor(i / 3) + Math.floor(j / 3)`. This way, we can easily check for any repeated numbers in these sections."

```javascript
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function(board) {
    const rows = Array.from({ length: 9 }, () => new Set());
    const cols = Array.from({ length: 9 }, () => new Set());
    const squares = Array.from({ length: 9 }, () => new Set());

    for (let i = 0; i < board.length; i++) {
        
        for (let j = 0; j < board[i].length; j++) {
            const num = board[i][j];

            if (num === '.') 
                continue;

            const m = Math.floor(j / 3);
            const n = Math.floor(i / 3);
            const k = 3 * m + n;

            if (rows[j].has(num) || cols[i].has(num) || squares[k].has(num))
                return false;

            rows[j].add(num);
            cols[i].add(num);
            squares[k].add(num);            
        }
    }
    
    return true;
};
```

- **Key Concept**: Checking for duplicates in each row, column, and 3x3 square.
- **Approach**: Use three hash tables to keep track of the numbers in rows, columns, and squares.
- **Key Phrases**:
    - "Three hash tables for rows, columns, and squares."
    - "Calculating square index with a formula."
    - "Identifying duplicates efficiently."
- **Time Complexity**: O(n^2), because we iterate through each cell of the 9x9 Sudoku board.
- **Space Complexity**: O(n), as we maintain three hash tables for the 9 rows, 9 columns, and 9 squares, and n refers to the total number of cells on the board.

```javascript
let squareIndex = 3 * Math.floor(i / 3) + Math.floor(j / 3);
if (hashTables[squareIndex].has(num)) return false;
```

### [128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)

Medium

To find the longest consecutive sequence in an array, we use a Set to hold the numbers as it helps speed up the search process. We start counting for a sequence only if the current number is the beginning of a sequence, meaning there's no previous consecutive number. Searching for an element within an array inside a loop can lead to O(n^2) time complexity.

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestConsecutive = function(nums) {
    let longest = 0;
    let set = new Set(nums);
    
    for (let i = 0; i < nums.length; i++) {
        if (!set.has(nums[i] - 1)) {
            
            let long = 0;
            
            while(set.has(nums[i] + long)) {
                long += 1;
            }

            longest = Math.max(long, longest);
        }
    } 

    return longest;
};
```

- **Key Concept**: Identifying if the current element is the start of a consecutive sequence.
- **Approach**: Use a `Set` to store the elements for quicker searches, **starting** the count for a sequence only when an element doesn't have a previous consecutive number.
- **Key Phrases**:
    - "Using a `Set` for efficient search."
    - "Counting starts from the sequence beginning."
    - "Avoiding O(n^2) complexity with array searches."

```javascript
let set = new Set(nums);
for (let num of nums) {
    if (!set.has(num - 1)) {
        // Start counting from this number
    }
}
```
