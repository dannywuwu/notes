Notes from the [Interview Quickstart](https://interviewquickstart.dev/) course


#  Arrays

## 2 pointers

- 2 pointers iterate through an array at the same time
- Useful for searching for pairs in a **sorted** array

### Example: Squares of a Sorted Array

Given an array of integers sorted in non-decreasing order, return an array of the squares of each number (also sorted in non-decreasing order)

`[-4, -1, 0, 3, 10] -> [0, 1, 9, 16, 100]`

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

### Big O

- Iterate over array once: O(n) time and O(1) space (no extra data structures)

### Questions

[Merge sorted array](https://leetcode.com/problems/merge-sorted-array/)

[2Sum 2](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

[3Sum](https://leetcode.com/problems/3sum/)

[Container with most water](https://leetcode.com/problems/container-with-most-water/)

[Trapping rainwater](https://leetcode.com/problems/trapping-rain-water/)
