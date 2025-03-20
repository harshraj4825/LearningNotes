## Two Pointer Algorithm
1. Opposite Direction (Left & Right Pointers)  
2. Same Direction (Slow & Fast Pointers)
#### Find a Pair with a Given Sum (Sorted Array):  
Given a sorted array and a target sum, find if there exists a pair of numbers that add up to the sum.  
```java
public boolean hasPairWithSum(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) return true;
        else if (sum < target) left++;
        else right--;
    }
    return false;
}
```
#### Remove Duplicates from a Sorted Array  
Given a sorted array, remove duplicates in-place and return the new length.  
```java
public int removeDuplicates(int[] arr) {
    if (arr.length == 0) return 0;
    int i = 0;
    for (int j = 1; j < arr.length; j++) {
        if (arr[j] != arr[i]) {
            i++;
            arr[i] = arr[j];
        }
    }
    return i + 1;
}
```
#### Container With Most Water  
Given an array height[], find two vertical lines such that they form a container that holds the maximum water.  
```java
public int maxArea(int[] height) {
    int left = 0, right = height.length - 1, maxArea = 0;
    while (left < right) {
        int area = (right - left) * Math.min(height[left], height[right]);
        maxArea = Math.max(maxArea, area);
        if (height[left] < height[right]) left++;
        else right--;
    }
    return maxArea;
}
```
#### Check If a String is a Palindrome  
Check if a given string is a palindrome (ignoring spaces and special characters).  
```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
        if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) return false;
        left++;
        right--;
    }
    return true;
}
```
## Sliding Window Algorithm
1. Fixed-Size Sliding Window
2. Variable-Size Sliding Window
#### Maximum Sum of K Consecutive Elements (Fixed-Size)  
Find the maximum sum of any K consecutive elements in an array.
```java
public int maxSumSubarray(int[] arr, int k) {
    int n = arr.length;
    if (n < k) return -1;  // Edge case
    int maxSum = 0, windowSum = 0;
    // Compute the sum of first 'k' elements
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    maxSum = windowSum;
    // Slide the window
    for (int i = k; i < n; i++) {
        // Add next element, remove first element
        windowSum += arr[i] - arr[i - k];  
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum;
}
```
#### Smallest Subarray with Sum ≥ S (Variable-Size)    
```java
public int minSubarrayLength(int S, int[] arr) {
    int minLength = Integer.MAX_VALUE, windowSum = 0, left = 0;

    for (int right = 0; right < arr.length; right++) {
        windowSum += arr[right]; // Expand window

        // Shrink window while sum is >= S
        while (windowSum >= S) {
            minLength = Math.min(minLength, right - left + 1);
            windowSum -= arr[left];  // Shrink from the left
            left++;
        }
    }

    return (minLength == Integer.MAX_VALUE) ? 0 : minLength;
}
```
#### Longest Substring Without Repeating Characters  
Find the length of the longest substring without repeating characters.  
```java
public int lengthOfLongestSubstring(String s) {
    Set<Character> charSet = new HashSet<>();
    int left = 0, maxLength = 0;

    for (int right = 0; right < s.length(); right++) {
        while (charSet.contains(s.charAt(right))) {
            charSet.remove(s.charAt(left));
            left++;
        }
        charSet.add(s.charAt(right));
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```
#### Longest Subarray with Sum ≤ K  
Find the longest contiguous subarray with a sum ≤ K.  
```java
public int longestSubarraySumAtMostK(int[] arr, int k) {
    int left = 0, windowSum = 0, maxLength = 0;

    for (int right = 0; right < arr.length; right++) {
        windowSum += arr[right];

        while (windowSum > k) {
            windowSum -= arr[left];
            left++;
        }

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```
## Kadane’s Algorithm  
Kadane's Algorithm is a Dynamic Programming (DP) approach to find the maximum sum of a contiguous subarray in an array of integers. It works in O(N) time complexity.  
#### Maximum Subarray Sum
Given an integer array arr[], find the contiguous subarray (containing at least one element) which has the maximum sum, and return this sum.  
```java
public static int maxSubarraySum(int[] arr) {
        // Stores the maximum sum found
        int maxSum = Integer.MIN_VALUE; 
        int currentSum = 0; // Tracks the sum of the current subarray

        for (int num : arr) {
            currentSum += num; // Add current element to the sum
            // Update max sum if needed
            maxSum = Math.max(maxSum, currentSum); 

            // If current sum becomes negative, reset it to zero
            if (currentSum < 0) {
                currentSum = 0;
            }
        }

        return maxSum;
    }
```
#### Finding the Subarray  
If you need to find the actual subarray that gives the maximum sum  
```java
public static int[] maxSubarray(int[] arr) {
        int maxSum = Integer.MIN_VALUE, currentSum = 0;
        int start = 0, end = 0, tempStart = 0;

        for (int i = 0; i < arr.length; i++) {
            currentSum += arr[i];

            if (currentSum > maxSum) {
                maxSum = currentSum;
                start = tempStart; // Update start index
                end = i; // Update end index
            }

            if (currentSum < 0) {
                currentSum = 0;
                tempStart = i + 1; // Move start index to next position
            }
        }

        // Extract the subarray
        int[] resultSubarray = new int[end - start + 1];
        System.arraycopy(arr, start, resultSubarray, 0, end - start + 1);

        return resultSubarray;
    }
```
