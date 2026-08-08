## 88. Merge Sorted Array

[leetcode link](https://leetcode.com/problems/merge-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150)

### Notes

increase `m` each time a new insert happens and remove the last element as well

we need to check 3 insertion types, l < r, l == r, l > r

l == r and l > r are the same, but in Python merge the conditional make the run slower

on the l < r scenario we have 2 options:

x. we can increase i only if possible (more options to check again l), if i < len(nums1)

x. we can insert only. if i is the last element on the l array, that means we can insert on right

we can insert in left only if is l > r but also if l == r, we reduce source code lines

at the beginning i was thinking this was a two pointers problem, but it wasn't

### Source code (watch it only if we can't find the solution)

<details>
    <summary align="left">Solution</summary>
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i, j = 0, 0
        

        while j < n:

            if nums1[i] < nums2[j]:

                if i < m:
                    i += 1
                else:
                    nums1.insert(i, nums2[j])
                    m += 1
                    j += 1
                    nums1.pop(-1)

            elif nums1[i] == nums2[j]:
                nums1.insert(i, nums2[j])
                m += 1
                j += 1
                nums1.pop(-1)

            elif nums1[i] > nums2[j]:
                nums1.insert(i, nums2[j])
                m += 1
                j += 1
                nums1.pop(-1)

        print('nums1', nums1)
```
</details>
