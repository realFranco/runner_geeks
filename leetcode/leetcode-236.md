## 236. Lowest Common Ancestor

[leetcode link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)

### Notes

i try it using an Array as input. The Challenge includes a binary tree representation.

use the "get parent" function `int(i/2)` to get the parent of a given node

store the parents

we need to store the indexes from p and q using a 1-based index,
the worst time complexity comes from this part as we are
searching on a list and not inside a binary tree

we need to run the "lowest common ancestor" (lca) two times

- 1st. one for q
- 2nd. one for q

on the 2nd. run, if the `i` exist in the `parents` set, that means
that during the `q` call, the lca is `i` because is already an ancestor
of `p`

`p` is an ancestor of `p`, same for `q`

### Source code (watch it only if we can't find the solution)

i got the solution after read the input on the leetcode challenges
in array mode and i remember that i saw the `int(i/2)` function to call
the parents on a heap, that's helps me to elaborate the solution

i need to recreate the solution but using this time a tree / graph

<details>
    <summary>Solution </summary>

```python
input = [

    # arr, p, q
    [[3,5,1,6,2,0,8,None,None,7,4], 5, 4],
    [[3,5,1,6,2,0,8,None,None,7,4], 6, 0],
    [[3,5,1,6,2,0,8,None,None,7,4], 5, 1],

]

def get_index(arr: list, x: int) -> int:
    i: int = 0
    while i < len(arr):
        if arr[i] == x:
            return i

        i += 1

    return -1

def lca(arr: list, i: int, parents: set, sol: bool, sol_i: int) -> (list | int):
    if i in parents:
        sol = True
        sol_i = i

        return parents, sol_i

    if i == 1:
        parents.add(i)

        return parents, sol_i

    parents.add(i)

    return lca(arr, int(i/2), parents, sol, sol_i)

def ext_lca(arr: list, p: int, q: int) -> None:

    p_i, q_i = 0, 0

    parents: set = set()

    sol_i = 0

    sol = False

    # Find p_i, q_i.

    p_i = get_index(arr, x=p)
    if p_i == -1:
        print('`p` not in `arr`')
        return
    p_i += 1 # We need 1 based-index.

    q_i = get_index(arr, x=q)
    if q_i == -1:
        print('`q` not in `arr`')
        return
    q_i += 1

    parents, _ = lca(arr, p_i, parents, sol, sol_i)

    # Check if `parents` is populated on this scope.

    parents, sol_i = lca(arr, q_i, parents, sol, sol_i)

    # print('> parents: ', parents)
    print('> p, q: ', p, q)
    # print('> sol_i: ', sol_i)
    print('> sol: ', arr[sol_i-1])
    print('')

    return

for t in input:
    ext_lca(
        arr=t[0],
        p=t[1],
        q=t[2]
    )
```

</details> 
