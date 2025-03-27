## Selection sort
Take unsorted array -> Iterate n-1 and pich smallest element and plact it as first
```java
privite void selectionsort(int[] arr){
  int n=arr.length;
  for(int i=0;i<n-1;i++){
      int smallest=arr[i];
      int sIndex=i;
      for(int j=i;j<n;j++){
        if(arr[j]<arr[i]){
          //swap it
          sIndex=j;
        }
      }
      arr[i] = arr[i] + arr[sIndex];
      arr[sIndex] = arr[i] - arr[sIndex];
      arr[i] = arr[i]- arr[sIndex];
  }
}
```  
