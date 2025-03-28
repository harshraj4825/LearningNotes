## Merge sort
- usally done recursive
- divie and conquer
```java
mergesort(int[] arr,int l, int r){
    if(l<h){
      mid=(l+r)/2;
      mergesort(arr,l,mid);
      mergesort(arr,mid+1,r);
      merge(arr,l,mid,r)'
    }
}
```
```java
merge(int[] arr, int l, int mid, int r){
  int[] tarr=new int[r-l+1];
  int p=0;

  int cu=0;
  int i=l;
  int j=mid+1;
  while(i<=mid && j<=r){
    if(arr[i]<=arr[j]){
        tarr[cu]=arr[i];
        cu++;
        i++;
    }else{
        tarr[cu]=arr[j];
        cu++;
        j++;
    }
  }
  while(i<=mid){
      tarr[cu]=arr[i];
      cu++;
      i++;
  }
  while (j<=r){
      tarr[cu]=arr[j];
      cu++;
      j++;
  }

  for(int k=0;k<tarr.length;k++){
      arr[l]=tarr[k];
      l++;
  }
}
```
