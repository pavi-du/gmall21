### 1.快速排序

首先以第一个数为基准，使用双指针,r右边的数都比基准大，l左边的数都比基准小

```java
class Solution{
    public void quickSort(int[] arr,int left,int right){
        
        int l = left;
        int r = right;
        int p = arr[l];
        if(l<r){
            while(l<r){
                while(l<r&&arr[r]>p){
                    r--;
                }
                if(l<r){
                    arr[l] = arr[r];
                    l++;
                }
                while(l<r&&arr[l]<p){
                    l++;
                }
                if(l<r){
                    arr[r] = arr[l];
                    r--;
                }
            }
            arr[l] = p;
            
            quickSort(arr,left,l-1);
            quickSort(arr,l+1,right);
        }
        
    }
}
```

### 2合并排序

排序的数组进行分，之后合并这俩个数组合并后保证有序。由于划分的边界是l<r,所以首先进行合并的是一个数组是一个数，之后进行回溯。

1，3，2，5，6

分

① 1，3，2      5，6
②1，3   2       5   6
③1   3   2    5   6

合并

④1，3   2    5,6
⑤1，2，3      5，6
⑥1，2，3，5，6

```java
 @Test
    public void test(){
        int[] arr = new int[]{1,5,4,3,5,3,6666};
        mergeSort(arr,0,arr.length-1);
        System.out.println(Arrays.toString(arr));
    }

    public void  mergeSort(int[] arr,int left,int right){
        if(left<right){
            int mid = (left+right)/2;
            mergeSort(arr,left,mid);
            mergeSort(arr,mid+1,right);
            merge(arr,left,mid,right);
        }
    }

    public void merge(int[] arr,int left,int mid,int right){
        int i  = left;
        int j = mid+1;
        int[] tmps = new int[right-left+1];
        int k = 0;
        while(i<=mid&&j<=right){
            if(arr[i]<=arr[j]){
                tmps[k++] = arr[i++];
            } else {
                tmps[k++] = arr[j++];
            }

        }
        while(i<=mid){
            tmps[k++] = arr[i++];
        }
        while (j<=right){
            tmps[k++] = arr[j++];
        }

        for(int tmp:tmps){
            arr[left++] = tmp;
        }
    }
```

### 3计数排序



```java
public class CountSort {

    @Test
    public void test(){
        int[] res = countSort(new int[]{1,3,-1,353,3});
        System.out.println(Arrays.toString(res));
    }

    public int[] countSort(int[] arr){

        int max = arr[0];
        int min = arr[0];
        for(int i = 1;i<arr.length;i++){
            if(arr[i]>max){
                max = arr[i];
            }
        }

        for(int i = 1;i<arr.length;i++){
            if(arr[i]<min){
                min = arr[i];
            }
        }

        int[] countArr = new int[max-min+1];
        for(int i :arr){
            countArr[i-min]+=1;
        }
        int tmp = 0;
        for(int i = 0;i<countArr.length;i++){
            tmp += countArr[i];
            countArr[i] = tmp;
        }

        int[] res  = new int[arr.length];
        for(int i = arr.length-1;i>=0;i--){
            res[countArr[arr[i]-min]-1] = arr[i];
            countArr[arr[i]-min]--;
        }
        return res;
    }
}
```

### 4.冒泡排序



```java
 public void bubbleSort(int[] arr){

        for(int i = 0;i<arr.length-1;i++){
            for(int j = 0;j<arr.length-i-1;j++){
                if(arr[j]>arr[j+1]){
                    int tmp = arr[j+1];
                    arr[j+1] = arr[j];
                    arr[j] = tmp;
                }
            }
        }
    }
```

### 5.插入排序

```java
 public void insertSortP(int[] arr){

        if(arr==null || arr.length==0){
            return;
        }

        int insertIndex = 0;
        int insertVlaue = arr[0];

        for(int i = 1;i<arr.length;i++){
            insertIndex = i;
            insertVlaue = arr[i];
            while (insertIndex>=1&&insertVlaue<arr[insertIndex-1]){
                arr[insertIndex] = arr[insertIndex-1];
                insertIndex--;
            }
            arr[insertIndex] = insertVlaue;
        }
    }
```

### 6.基数排序



```java
 public static void redixSort(int[] arr) {
        int[][] bucket = new int[10][arr.length];

        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        int count = 0;
        for (; max != 0; max /= 10) {
            count++;
        }

        int[] bucketCounts = new int[10];
        for (int i = 0, n = 1; i < count; i++, n *= 10) {
            for (int j = 0; j < arr.length; j++) {
                bucket[arr[j] / n % 10][bucketCounts[arr[j] / n % 10]] = arr[j];
                bucketCounts[arr[j] / n % 10]++;
            }

            int index = 0;
            for (int t = 0; t < bucket.length; t++) {
                for (int k = 0; k < bucketCounts[t]; k++) {
                    arr[index] = bucket[t][k];
                    index++;
                }
            }

            for (int j = 0; j < bucketCounts.length; j++) {
                bucketCounts[j] = 0;
            }

        }

    }
```

