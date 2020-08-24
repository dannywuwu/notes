# Merging

- The process of combining 2 sorted lists into a single sorted list

Suppose we have 2 sorted lists A, B and new list C,  we want to create a new sorted list C by comparing elements from A and B

1. Use 2 pointers to iterate through A and B
2. If the current A element is smaller than the current B element, add the current A element to C. If not, add element B to C
3. Repeat step 2 until we finish one of the lists
4. Append the unfinished list to C, as all of its elements are greater than the elements of C and so C remains sorted
5. C is now a sorted merge of A and B

- O(m + n), where m + n are the size of A and B
    - Simplifies to O(n)

## n-way merging
   
- If we wanted to merge n sorted lists, we can use n pointers to iterate through the lists and compare elements throughout all lists
- Or we can perform 2-way merging by comparing pairs of n lists
- There are many different patterns of merging

# 2-way merge sort

- Not to be confused with merge-sort
    - 2-way merge sort is iterative, while merge sort is recursive

1. Assume that each element in the list is a list of size 1, which means that they are already sorted
    - Merging requires sorted lists, which we have!
2. Compare each 'list' with the next 'list' - If the next 'list' is larger, swap them
    - If there is an odd number of elements, do not worry about the last element. It will be merged later
3. Merge the two elements into a list. If we previously had n lists, we now have n/2 lists in this iteration.
4. Repeat until we have merged everything into 1 list

- For intermediate storage, we can use 2 lists and alternate between them
- O(nlogn) time, O(n) space

# Merge Sort

- Divide and conquer
- Break into 2 subproblems - left and right subarrays

```python
def mergesort(l, h):
    # at least 2 elements
    if l < h:
        mid = l + (h - 1)//2
        mergesort(l, mid)
        mergesort(mid + 1, h)
        merge(l, mid, h)
```

