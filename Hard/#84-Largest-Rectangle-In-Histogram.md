Given an array of integers heights representing the histogram's bar `height` where the width of each bar is `1`, return *the area of the largest rectangle in the histogram*.

 

__Example 1:__

<img src="../src/Asset/histogram%20ex-1.jpg" width="600" height="220">

```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
```

__Example 2:__

<img src="../src/Asset/histogram-ex-2.jpg" width="180" height="280">

```
Input: heights = [2,4]
Output: 4
``` 

__Constraints:__

* `1 <= heights.length <= 105`
* `0 <= heights[i] <= 104`

```javascript
/**
 * @param {number[]} heights
 * @return {number}
 */
/**
 * @param {number[]} heights
 * @return {number}
 */

const largestRectangleArea = function(heights) {

  const len = heights.length;
  const stack = [];
  let max = 0;
  let h = 0;
  let w = 0;
  
  for (let i = 0; i <= len; i++) {
      
    while (stack.length && (i === len || heights[i] <= heights[stack[stack.length - 1]])) {
      h = heights[stack.pop()];
      w = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      max = Math.max(max, h * w);
    }
    stack.push(i);
  }
  
  return max;
};
```