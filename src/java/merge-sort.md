# Merge Sort
A Divide and Conquer algorithm.

## Divide
- Divide the input array into 2 halves, using the midpoint as a "*pivot* ".
- Recursively call the sorting portion of the algorithm until the original array that has been passed into the function can no longer
be divided.

```java
public class MergeSort {
    public void mergeSort(int[] inputArr) {
        int arrLen = inputArr.length;

        if (arrLen < 2) {
            return;
        }

        int midpoint = arrLen / 2;
        int[] leftArr = new int[midpoint];
        int[] rightArr = new int[arrLen - midpoint];

        for (int i = 0; i < midpoint; i++) {
            leftArr[i] = inputArr[i];
        }

        for (int i = midpoint; i < arrLen; i++) {
            rightArr[i - midpoint] = inputArr[i];
        }

        //TODO: Recursively call mergeSort on left and right arrays
        mergeSort(leftArr);
        mergeSort(rightArr);

        //TODO: Call merge function
        System.out.println(merge(inputArr, leftArr, rightArr));
    }
}
```

- For edge case testing, we check the length of the array that is passed in to determine if there is any work to be done.
If the length is less than 2, the array is technically sorted and the algorithm should not be performed.