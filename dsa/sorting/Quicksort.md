## Quick Sort (D & C algorithm)
Quick sort is a divide-and-conquer sorting algorithm that works selecting the pivot element and partitioning the array in a such that smaller than the pivot are placed left, and greater than the pivot are placed right.  
**Steps of Quick sort**  
1. Choose a pivot (e.g, 1st, last, middle, or random)
2. Partiton the array:
   - Place elements smaller than the pivot to its left.
   - Place elements greater than the pivot to its right.
3. Recurisvely apply quick sort to the left and right subarrays.

```java
void quicksort(int[] arr, int low, int high)
{
  if(low<high){
      int pivotIndex= partition(arr,low,high);
      quickSort(arr,low,pivotIndex-1);
      quickSort(arr,pivotIndex,high);
  }
}
```
```java
int partition(int[] arr,int low, int high){
  int pivot=arr[high];//Choosing the last element as pivot
  int i=low-1; //pointer for smaller elements
  for(int j=low;j<high;j++){
    if(arr[j]<pivot){
      i++;
      swap(arr,i,j);
    }
  }
  swap(arr,i+1,high);
  return i+1;
}
```
