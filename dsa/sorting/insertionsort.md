## Insertion sort  
Pick an element and place in sorted arr
```java
private void insertionsort(int[] arr){
  for(int i=1;i<n;i++){
    int curr=i;
    int prev=i-1;
     while(prev>=0 && arr[prev]>arr[curr]){
        arr[prev+1]=arr[prev];
        prev--;
    }
    arr[prev+1]=curr;
  }
}
```
