Notes from the [Interview Quickstart](https://interviewquickstart.dev/) course


#  Arrays

## 2 pointers

- 2 pointers iterate through an array at the same time
- Useful for searching for pairs in a **sorted** array

### Example: Squares of a Sorted Array

> Given an array of integers sorted in non-decreasing order, return an array of the squares of each number (also sorted in non-decreasing order)

`[-4, -1, 0, 3, 10] -> [0, 1, 9, 16, 100]`

**Answer**
 
1. Have both pointers start on the absolute lowest number (in this case 0)
2. Move 1 pointer to the left, 1 pointer to the right
3. Compare both pointed values, appending the smaller squared one to the result
4. Move the pointer pointing to the lower value once again in the direction it was going in 
5. Compare once more
6. Repeat 3-5 until finished

```markdown
      *     *
[-4, -1, 0, 3, 10] -> []

  *         *
[-4, -1, 0, 3, 10] -> [1]

 *             *
[-4, -1, 0, 3, 10] -> [1, 9]

...
```

- Iterate over array once: O(n) time and O(1) space (no extra data structures)

### Questions

[Merge sorted array](https://leetcode.com/problems/merge-sorted-array/)

[2Sum 2](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

[3Sum](https://leetcode.com/problems/3sum/)

[Container with most water](https://leetcode.com/problems/container-with-most-water/)

[Trapping rainwater](https://leetcode.com/problems/trapping-rain-water/)

## Hash Maps

- O(1) insert/get/delete 
- Detect duplicates and count occurrences of array elements
- Reduce time complexity 

**Duplicate, Unique, # Occurences -> Hashmaps**

### Example: Two Sum

> Given an array of integers, return True if there are 2 numbers that add up to a specified target number

`[2, 7, 9] -> 16`

**Answer: Hash Set**

1. Hash the current element by `target - element`
2. If the hash exists in the set, return True
3. Else, move on to the next element

```markdown
2: is 14 in the hash set? No
{2, }

7: is  9 in the hash set? No
{2, 7}

9: is 7 in the hash set? Yes
True
```

- O(n) runtime and O(n) space

### Questions

[First unique character](https://leetcode.com/problems/first-unique-character-in-a-string/)

[Isomorphic strings](https://leetcode.com/problems/isomorphic-strings/)

[Insert/delete/random](https://leetcode.com/problems/insert-delete-getrandom-o1/)