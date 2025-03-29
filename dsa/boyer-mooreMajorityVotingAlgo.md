## Q. Given an array nums of size n, return the majority element that have more than N/ 2 occurrences.  
TC=O(N) ,SC= O(1)  

This algorithm works on the fact that if an element occurs more than N/2 times, it means that the remaining elements other than this would definitely be less than N/2. So let us check the proceeding of the algorithm.  
- First, choose a candidate from the given set of elements if it is the same as the candidate element, increase the votes. Otherwise, decrease the votes if votes become 0, select another new element as the new candidate.
- Steps to implement the algorithm :
**Step 1 – Find a candidate with the majority –**  

- Initialize a variable say i ,votes = 0, candidate =-1 
- Traverse through the array using for loop
- If votes = 0, choose the candidate = arr[i] , make votes=1.
- else if the current element is the same as the candidate increment votes
- else decrement votes.

**Step 2 – Check if the candidate has more than N/2 votes –**

- Initialize a variable count =0 and increment count if it is the same as the candidate.
- If the count is >N/2, return the candidate.
- else return -1.  
```java
  // Function to find majority element
  public static int findMajority(int[] nums)
  {
    int count = 0, candidate = -1;

    // Finding majority candidate
    for (int index = 0; index < nums.length; index++) {
      if (count == 0) {
        candidate = nums[index];
        count = 1;
      }
      else {
        if (nums[index] == candidate)
          count++;
        else
          count--;
      }
    }

    // Checking if majority candidate occurs more than
    // n/2 times
    count = 0;
    for (int index = 0; index < nums.length; index++) {
      if (nums[index] == candidate)
        count++;
    }
    if (count > (nums.length / 2))
      return candidate;
    return -1;

    // The last for loop and the if statement step can
    // be skip if a majority element is confirmed to
    // be present in an array just return candidate
    // in that case
  }
```
