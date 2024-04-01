# Find the largest difference

The link: https://bigfrontend.dev/problem/Find-the-largest-difference

Given an array of numbers, pick any two numbers a and b, we could get the difference by Math.abs(a - b).

Can you write a function to get the largest difference?

```javascript
largestDiff([-1, 2,3,10, 9])
// 11,  obviously Math.abs(-1 - 10) is the largest

largestDiff([])
// 0

largestDiff([1])
// 0
```



Code:

```javascript
 function largestDiff(result) {
  if (!result.length) return;
  return Math.abs(Math.max(...result) - Math.min(...result)); 
}
```

we can get the max value and the min value by using Math.max and Math.min, then we can calculate the difference between max and min by using Math.abs;



```javascript
  function largestDiff(arr) {
     if (arr.length === 0) return 0;
     let min = Infinity; // to record the min value;
     let max = -Infinity; // to record the max value;
     let result = Infinity; // to record the difference between max and min;
     for (let item of arr) {
       if (item < min) {
         min = item;
         result = max - min;
       }
       if (item > max) {
         max = item;
         result = max - min;
       }
     }
     return result;
}
```



1. If the length of passed-in parameter is 0, we'll return 0;

2. We can use for of loop to traverse the array, if the current item is smaller than the min value, we'll update the min value, and calculate the difference  between max and min, then assign it to the result;

3. If the current item is larger than the max value , we'll update the max value, and update  the difference between max and min, then assign it to the result;

4. At last, we'll return the result;