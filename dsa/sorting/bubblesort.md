## Bubble Sort  

Theory: In (n-1) iteration -> compare adjecent element and swap it -> do it for each element.  
**In First iteration the larger element pushed to end**
```java
privite void bubblesort(int[] arr){
  int n=arr.length;
  for(int i=0;i<n;i++){
      for(int j=0;j<n-i-1;j++){
        if(arr[j]>arr[j+1]){
          //swap it
          arr[j] = arr[j] + arr[j+1];
          arr[j+1] = arr[j] - arr[j+1];
          arr[j] = arr[j]- arr[j+1];
        }
      }
  }
}
```
#### Optimisation in bubble sort  
add extra check isSwap.  
```java
privite void bubblesort(int[] arr){
  int n=arr.length;
  for(int i=0;i<n;i++){
      boolean isSwap=false;
      for(int j=0;j<n-i-1;j++){
        if(arr[j]>arr[j+1]){
          //swap it
          arr[j] = arr[j] + arr[j+1];
          arr[j+1] = arr[j] - arr[j+1];
          arr[j] = arr[j]- arr[j+1];
          isSwap=true;
        }
      }
      if(!isSwap)return;
  }
}
```
