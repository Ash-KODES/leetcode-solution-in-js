Given the `root` of a binary tree, *determine if it is a valid binary search tree (BST)*.

A __valid BST__ is defined as follows:

* The left subtree of a node contains only nodes with keys __less than__ the node's key.
* The right subtree of a node contains only nodes with keys __greater than__ the node's key.
* Both the left and right subtrees must also be binary search trees.
 

__Example 1:__

<img src="../src/Asset/tree-ex-1.jpg" width="400" height="220">

```
Input: root = [2,1,3]
Output: true
```

__Example 2:__

<img src="../src/Asset/tree-ex-2.jpg" width="400" height="220">

```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
``` 

__Constraints:__

* The number of nodes in the tree is in the range `[1, 104]`.
* `-231 <= Node.val <= 231 - 1`

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */

var isValidBST = function(root) {
    return helper(root, null, null);
}

function helper(node, low, high) {
    if (node === null) return true;
    const val = node.val;
    if ((low !== null && val <= low) || (high !== null && val >= high)) 
        return false;
    return helper(node.right, val, high) && helper(node.left, low, val);
}
```