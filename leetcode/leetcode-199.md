## 199. Binary Tree Right Side View

[leetcode link](https://leetcode.com/problems/binary-tree-right-side-view/)

### Notes

i use a post order traversal on the tree

use a auxiliar variable `h` to measure the tree `height` each new recursive call
it turns into `h+1`

we use a list object (pass it as reference due the Python first-order class)
each `h` is an entry in that list, for example a tree with h=3 means

`[ [], [] ,[] ]` each inner list is a level

once the level order traversal ends, we want to read each level, but extract
the last element on those list, with is belongs the right-most value on each list

### Source code (watch it only if we can't find the solution)

<details>
    <summary>Solution </summary>

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def level_order(self, node: TreeNode | None, h: int, lvl: list[list]) -> None:

        if node is None:
            return

        if len(lvl) < h:
            lvl.append([])

        self.level_order(node.left, h+1, lvl)

        self.level_order(node.right, h+1, lvl)

        lvl[h-1].append(node.val)
    
    def rightSideView(self, root: TreeNode | None) -> list[int]:
        
        lvl: list[list[int]] = []
        h: int = 1
        self.level_order(root, 1, lvl)

        out: list[int] = [ladder[-1] for ladder in lvl]
        # print(out)

        return out
```

</details> 
