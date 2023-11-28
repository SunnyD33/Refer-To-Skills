# Binary Search
***Time Complexity: O (log n)***

- This algorithm can be used in place of linear search and in some cases, have a better use case based on 
  the type of data structure that is being searched against.
- Linear search is still a good option but in some cases, binary search can be better from a performance perspective 
  as both rely on the amount of inputs in the structure. For Binary Search, it can have fewer iterations to 
  completion than linear search but this should be dependent on the size of the structure. For this example, we are 
  going to use an array.
- Binary Search uses a midpoint value to determine if it is the target that is being looked for or to detemine which 
  side of the array that the target should be on. We say should be as the target may not exist in the array, but we 
  still know where it should be if it was.

```java
int[] nums = {-1,0,3,5,9,12};
```
Here we have an array of integers, that are sorted. Please note, that this algorithm must be run on a collection 
that is sorted, or you will get unexpected outcomes.

- Breaking this down, we start by having a function that returns an integer in this case and takes in two parameters, 
an integer array and a target that we are trying to find.
- We then create two variables that control the endpoints of our search space, lo and hi. Since we are dealing with 
  an array, we can set ```lo``` to be 0 (the first index of the array) and ```hi``` to the length of the array - 1 (the 
  last index of the array).

```java
    public int search(int[] arr, int target) {
        int lo = 0;
        int hi = arr.length - 1;
```
- We want to use the midpoint to determine if the midpoint is indeed our target or if the target is in the vicinity 
  of our endpoints. Since we are going to change the endpoints based on where the target is in relation to the 
  midpoint, we want to create a ```mid``` variable and update it while searching if the target is not found at the 
  midpoint.

```java
        while(lo <= hi) {
            int mid = (int) Math.floor(lo + ((double) (hi - lo) / 2 ));
```

- We needed to do some casting here because we want an integer as it is easier to ensure that we will get whole 
numbers, especially when getting the midpoint. We don't have indexes in arrays that are not whole numbers, so this 
will cover that.

- Also note the <= in the while loop. We can run this with just < BUT <= helps with the caveat of an array with one 
  element in it. It's an off chance that will happen but...edge cases..


- For the final piece, we check the midpoint within the while loop. If the midpoint's value in the array happens to 
  match the target value, then we are done! We return the value of the midpoint variable.
- If the midpoint's value in the array does not match the target, then we need to consider where the target is 
  compared to the midpoints current location. Since binary search can basically half an array with one iteration, we 
  must tell the algorithm which way to look where the target should be.
  - If the target is greater than midpoints current value, since the array is sorted, we know that our value should 
    be to the right of the current midpoint. Should that be the case, we need to move our lo value to our current 
    midpoint + 1. We don't want to include the current midpoint as part of the lo since we already know that it is 
    not the target.
  - If the target is less than the midpoints current value, and with the array being sorted, we know that our value 
    is less than the midpoint. In this case, we need to bring the hi down to the current midpoint - 1. Since we know 
    that midpoint is not our target, we do not need to include it as part of the hi value.


- Note that the midpoint will always get updated as long as the while loop is true, so with the definition of the 
  variable where it is, we can be sure that the midpoint will update based on an updated lo or hi value.
- 

- If all else should fail, then we return a -1 to appease the function call that it must return an integer. When we 
  get a -1, we should assume that the target value that was passed in the function was not in the array.

```java
            if(arr[mid] == target) {
                return mid;
            } else if (arr[mid] > target) {
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
```

## Full Binary Search Solution


```java
    public int search(int[] arr, int target) {
        int lo = 0;
        int hi = arr.length - 1;

        while(lo <= hi) {
            int mid = (int) Math.floor(lo + ((double) (hi - lo) / 2 ));

            if(arr[mid] == target) {
                return mid;
            } else if (arr[mid] > target) {
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
        }

        return -1;
    }
```