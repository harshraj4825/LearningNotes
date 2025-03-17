## Steps of the Divide and Conquer Algorithm  
1. Divide: Break the problem into smaller subproblems.  
2. Conquer: Solve the subproblems recursively.  
3. Combine: Merge the results to solve the original problem.

Exampeles: Merge Sort, Quick Sort, Binary Search, Strassen’s Matrix Multiplication, Closest Pair of Points
#### Merge Sort
```
MERGE_SORT(arr, left, right)
    if left < right
        mid = (left + right) / 2
        MERGE_SORT(arr, left, mid)   // Sort first half
        MERGE_SORT(arr, mid+1, right) // Sort second half
        MERGE(arr, left, mid, right)  // Merge both halves

MERGE(arr, left, mid, right)
    Create temporary arrays L and R
    Copy data from arr[left...mid] to L and arr[mid+1...right] to R
    Merge L and R back into arr[left...right]

```
