## 14. Longest Common Prefix

[leetcode link](https://leetcode.com/problems/longest-common-prefix/description/?envType=study-plan-v2&envId=top-interview-150).

### Notes

check the longest string (`n`)

create a matrix `n x n`, if the word is smaller than `n` insert empty chars `''`

iterate the matrix, column by column, if found an `''` break the internal cycle

if the inner cycle counter ends with size `n`, the char in the iteration is a valid prefix

if there is no more continuity break the external cycle

continuity means tha the previous iteration results is the same as the curren iteration result

### Source code (watch iif we can't recreate the solution)

<details>
    <summary>Solution </summary>

```python
# Big O: O(n x n)
# Where `n` is the size of the longest string.

# Space complexity: O(n x n) as we are using a matrix (we are not counting other objects).

class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        data_n: int = len(strs)

        big_word: int = max([len(_) for _ in strs])

        matrix: List[ List[str] ] = [
            [word[j] if j < len(word) else '' for j in range(0, big_word)]
            for word in strs
        ]

        preffix_set: str = ''
        previous_n: int = 0
        c_n: int = 0

        for j in range(0, big_word):

            previous_n = c_n
            c_n = 0
            for i in range(0, data_n):

                if matrix[i][j] == '':
                    break

                if strs[0][j] == strs[i][j]:
                    c_n += 1

            if j > 0 and previous_n != c_n:
                break

            if c_n == data_n:
                preffix_set += strs[0][j]

        return preffix_set
```
</details>
