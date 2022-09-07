# Merge Sort (Java)
A Divide and Conquer algorithm.

***Time Complexity: O(nlogn)***

## Divide
- Divide the input array into 2 halves, using the midpoint as a "*pivot* " via the ```sort``` function.
- Recursively call the sorting portion of the algorithm until the original array that has been passed into the function can no longer
be divided.

- For edge case testing, we check the length of the array that is passed in to determine if there is any work to be done. ``````int arrLen = inputArr.length;``````
If the length is less than 2, the array is technically sorted and the algorithm should not be performed.
```java
        if (arrLen < 2) {
            return;
        }
```
- If we have an array that has more than 2 items, we will need to first start by dividing the array into 2 halves. This is best done by creating a midpoint of the passed in array,
which can be found by doing integer division on the length of the array divided by 2, ```int midpoint = arrLen / 2;```.
This midpoint will be used to determine the length of a left array and a right array that will be filled with the values from the passed array. Integer division is needed for whole numbers for a "clean" split.
- The length of the left array will be the midpoint that was found from the passed array, ```int[] leftArr = new int[midpoint]```. For example, if the passed ```array.length = 5```, and the length
is divided by 2, the midpoint would be 2. So the left array would be initialized with the length of 2. We would then need to initialize the length of the right array with the remaining values.
We would determine the remaining values using the midpoint variable that was created and subtract that value from the length of the passed array. ```int[] rightArr = new int[arrLen - midpoint];```
- Once the length of each array has been found, each respective array will need to be filled with left side and right side of the passed array.
```java
        for (int i = 0; i < midpoint; i++) {
            leftArr[i] = inputArr[i];
        }

        for (int i = midpoint; i < arrLen; i++) {
            rightArr[i - midpoint] = inputArr[i];
        }   
```
- The ```sort``` function will then be recursively called until the passed array is split down as small as it can before work should not be performed on the left and right arrays.
```java
        sort(leftArr);
        sort(rightArr);
```
- The ```merge``` helper function is then called to take the smaller arrays, which will be sorted, and merge them into one final sorted array. The ```merge``` function will compare the values of the left and right arrays determine the order in which they are added to the final array while walking (iterating) through the left and right array.
```java
        merge(inputArr, leftArr, rightArr);
```

 ***Sort Function Example***

```java
    public void sort(int[] inputArr) {
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

        //TODO: Recursively call sort on left and right arrays
        sort(leftArr);
        sort(rightArr);

        //TODO: Call merge function
        merge(inputArr, leftArr, rightArr);
    }
```

## Conquer
- Sort and merge the divided arrays
- The ```merge``` helper function will take in the initial array that was passed into ```sort``` and the left and right arrays are passed in as well. 
```java
    private void merge(int[] array, int[] left, int[] right)
```
- To iterate through each array, we can create three integer variables for each of the array's. This will make it easier to keep track of where each array is while walking through the left and right arrays and also making sure that the final array is only being stepped through after we choose which is the correct element to add to it.
```java
    int i = 0, j = 0, k = 0;
```
*'*i will be used for the left array, j will be used for the right array and k will be used for the passed in array that will hold the final sorted array*'*

- We use a while loop to check that the left and the right array have values in them to be compared. When one of the arrays run out of values, we will no longer need to compare the values, so the while loop should stop. During the while loop, we will compare the values of each the left and right array via the iterator variables that we created, and pass the smaller of the two values into the final array.
```java
    // TODO: Compare the left and right arrays to begin sorting main array
    while(i < left.length && j < right.length) {
        if(left[i] < right[j]) {
            array[k++] = left[i++];
        } else {
            array[k++] = right[j++];
        }
    }
```
- Note: We only need to update the index of the left and right array when the value from the respective array (left or right) has been added to the final array. The final array index will increment at the same time that a value as been added to it. For example, the initial condition of ```array[k++] = left[i++];``` is showing that the final ```array[k]``` will hold the value of ```left[i]``` and then ```i``` will increment. Once the value has been added to the ```array```, ```k``` increments. This logic holds true if the value of the right array is smaller than the value of the left array as well, with ```j``` incrementing after that value is stored from the right array.
- We then have to account for the fact that one array may put all of its values in the final array before the other, so we will need to create two separate while loops to check both the left and the right arrays separately to check if there are any values left that need to be added into the final array.

```java
    // TODO: Check to see if there are any values left in one of the arrays if one array is done being added to the final array
    while(i < left.length) {
        array[k++] = left[i++];
    }

    while(j < right.length) {
        array[k++] = right[j++];
    }
```

- Once we have checked that both arrays have been compared and all values of each array are saved into the final array, the merge sort algorithm is complete!

***Merge Helper Function Example***
```java
    private void merge(int[] array, int[] left, int[] right) {
        // TODO: Create variables to track the index of each passed array
        int i = 0, j = 0, k = 0;

        // TODO: Compare the left and right arrays to begin sorting main array
        while(i < left.length && j < right.length) {
            if(left[i] < right[j]) {
                array[k++] = left[i++];
            } else {
                array[k++] = right[j++];
            }
        }

        // TODO: Check to see if there are any values left in one of the arrays if one array is sorted
        while(i < left.length) {
            array[k++] = left[i++];
        }

        while(j < right.length) {
            array[k++] = right[j++];
        }
    }
```

## Full Merge Sort Java solution
```java
public class MergeSort {

    public void sort(int[] array) {
        if (array.length < 2) {
            return;
        }

        // TODO: Create variables for the midpoint and the two int arrays
        int midpoint = array.length / 2;
        int[] left = new int[midpoint];
        int[] right = new int[array.length - midpoint];

        // TODO: Fill the array with their respective halves using two for loops
        for (int i = 0; i < midpoint; i++ ) {
            left[i] = array[i];
        }

        for (int i = midpoint; i < array.length; i++) {
            right[i - midpoint] = array[i];
        }

        // TODO: Call method recursively on the left and right arrays
        sort(left);
        sort(right);

        // TODO: Call merge helper method to merge left and right arrays with the main array
        merge(array, left, right);
    }

    private void merge(int[] array, int[] left, int[] right) {
        // TODO: Create variables to track the index of each passed array
        int i = 0, j = 0, k = 0;

        // TODO: Compare the left and right arrays to begin sorting main array
        while(i < left.length && j < right.length) {
            if(left[i] < right[j]) {
                array[k++] = left[i++];
            } else {
                array[k++] = right[j++];
            }
        }

        // TODO: Check to see if there are any values left in one of the arrays if one array is sorted
        while(i < left.length) {
            array[k++] = left[i++];
        }

        while(j < right.length) {
            array[k++] = right[j++];
        }
    }
}
```