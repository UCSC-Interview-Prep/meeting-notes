# Nikita and String

## [Problem Statement][1]:
```
One day Nikita found the string containing letters "a" and "b" only.

Nikita thinks that string is beautiful if it can be cut into 3
strings (possibly empty) without changing the order of the letters,
where the 1-st and the 3-rd one contain only letters "a" and the 2-nd
contains only letters "b".

Nikita wants to make the string beautiful by removing some
(possibly none) of its characters, but without changing their order.
What is the maximum length of the string he can get?
```
## [Solution][2]:
```python
def max_beautiful_len(s):
  """This function returns the maximum length of a beautiful string
  created
  from a given string.

  Time Complexity: O(len(s)**2)
  Space Complexity: O(len(s))
  """
  # Let's get the prefix sums for a and b, respectively.
  prefix_a = prefix_sum(int(el == 'a') for el in s)
  prefix_b = prefix_sum(int(el == 'b') for el in s)

  # Let i and j be the boundaries for our 1st and 3rd strings,
  # respectively; we can calculate the beautiful length
  # for every (i, j) pair.
  n = len(s)
  max_len = 0
  for i in xrange(n+1):
    for j in xrange(i, n+1):
      curr_len = (prefix_a[i] + prefix_b[j]-prefix_b[i] +
                  prefix_a[n]-prefix_a[j])
      max_len = max(max_len, curr_len)
  return max_len

def prefix_sum(alist):
  """This function returns the prefix sum for a list of ints.

  Time Complexity: O(len(alist))
  Space Complexity: O(len(alist)) but could be done in-place in O(1)
  """
  result = [0]
  for el in alist:
    result.append(el+result[-1])
  return result


s = raw_input()
print max_beautiful_len(s)
```


[1]: http://codeforces.com/contest/877/problem/B
[2]: http://codeforces.com/blog/entry/55362
