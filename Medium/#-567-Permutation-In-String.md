### Given two strings s1 and s2, return true if s2 contains a permutation of s1, or false otherwise.

#### In other words, return true if one of s1's permutations is the substring of s2.

 
__Example 1:__
```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```

__Example 2:__
```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
``` 

__Constraints:__

* 1 <= s1.length, s2.length <= 104
* s1 and s2 consist of lowercase English letters.

```javascript
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var checkInclusion = function(s1, s2) {
  if (s1.length > s2.length) return false
  var floatingMap = new Map();
  var floatingSum = 0;
  var checkMap = new Map();
  var checkSum = 0;
  
  for (var i = 0; i < s1.length; i++) {
    checkSum += s1.charCodeAt(i);
    const count = checkMap.get(s1.charAt(i)) || 0;
    checkMap.set(s1.charAt(i), count + 1);
  }

  for(var i = 0; i < s2.length; i++) {
    if (i >= s1.length) {
      var ch = s2.charAt(i - s1.length);
      var count = floatingMap.get(ch);
      floatingMap.set(ch, count - 1);
      const chCode = s2.charCodeAt(i - s1.length);
      floatingSum -= chCode;
    }
    
    var ch = s2.charAt(i);
    var count = floatingMap.get(ch) || 0;
    floatingMap.set(ch, count + 1);
    const chCode = s2.charCodeAt(i);
    floatingSum += chCode;
        
    if (floatingSum === checkSum) {
      var isFound = true;
      checkMap.forEach((value, key) => {
        if (floatingMap.get(key) !== value) {
          isFound = false;
          return;
        }
      });
        if (isFound) {
        return true;
      }
    }
  }

  return false;
};
```
