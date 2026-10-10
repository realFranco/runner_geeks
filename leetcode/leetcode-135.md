## 135. Candy

[leetcode link](https://leetcode.com/problems/candy/description/?envType=study-plan-v2&envId=top-interview-150)

### Notes

is a minimization problem, that's why we need to share the small amount of candies

the first iteration is from left to right, on each iteration we compare with the
left neighbor, value with higher rating will take `+1` from the lower rating

`candies[i] = candies[i-1] + 1`

the second iteration is from right to left, on each iteration we compare with the
right neighbor, on this case we need to took the max between those values
the right neighbor will take `+1` before make the `max()`

`max(min_candies[i], min_candies[i+1] + 1`

the return will be the sum of the candies

#### Improvement

we discover that if the array contains only increasing values, `1,3,5,7 ...` there is
no need to conduct the 2nd. iteration

### Source code (watch it only if we can't find the solution)

i got the solution from NeetCode after fails under several trials, my solution was quite
similar but i ran out of time

[YouTube video](https://www.youtube.com/watch?v=1IzCRCcK17A&t=597s)

<details>
    <summary>Solution </summary>

```python
tests = [
    [1,2,3,4], # 10

    [1, 2, 3, 2, 1], # 9

    [1, 3, 4, 5, 2], # 11

    [1, 2, 5, 4, 3, 2], # 14

    [1, 4, 3, 2, 1, 2, 3, 4], # 20
]


def candy(ratings: list[int]) -> int:
    n = len(ratings)

    min_candies: list[int] = [1] * n

    i = 0
    for i in range(1, n):
        if ratings[i-1] < ratings[i]:
            min_candies[i] = min_candies[i-1] + 1        
        i += 1

    for i in range(n-2, -1, -1):
        if ratings[i] > ratings[i+1]:
            min_candies[i] = max(min_candies[i], min_candies[i+1] + 1)
        i -= 1

    return sum(min_candies)

def candy_upgrade_it(ratings: list[int]) -> int:
    n = len(ratings)
    
    min_candies: list[int] = [1] * n

    decreasing_hits: int = 0

    # We skip the first comparison, that's why we compare in here.
    if n > 1 and ratings[0] > ratings[1]:
        decreasing_hits += 1
    
    for i in range(1, n):
        if i < n-1 and ratings[i] > ratings[i+1]:
            decreasing_hits += 1

        if ratings[i-1] < ratings[i]:
            min_candies[i] = min_candies[i-1] + 1
        
        i += 1

    # If no decreasing sequence, no need to make the 2nd. iteration.
    if decreasing_hits > 0:
        for i in range(n-2, -1, -1):
            if ratings[i] > ratings[i+1]:
                min_candies[i] = max(min_candies[i], min_candies[i+1] + 1)
            i -= 1

    return sum(min_candies)

for test in tests:
    print('> in', test)
    # out = candy(ratings=test)
    out = candy_upgrade_it(ratings=test)
    print('> out', out)
    print('\n')
```
</details>
