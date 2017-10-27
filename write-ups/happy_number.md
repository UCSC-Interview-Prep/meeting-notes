# Happy Number

## [Problem Statement][1]:
```
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with
any positive integer, replace the number by the sum of the squares of its
digits, and repeat the process until the number equals 1 (where it will
stay), or it loops endlessly in a cycle which does not include 1. Those
numbers for which this process ends in 1 are happy numbers.
```
## [Solution][2]:
```python
class Solution(object):
    def isHappy(self, n):
        """This function returns a boolean indicating whether a given number
        is happy.

        Time Complexity: ?
        Space Complexity: O(1)
        """
        if n <= 0:
            return False

        # We can solve this using the Floyd cycle detection algo
        # https://en.wikipedia.org/wiki/Cycle_detection#Floyd.27s_Tortoise_and_Hare
        slow = n
        fast = digit_square_sum(n)
        while slow != fast:
            slow = digit_square_sum(slow)
            fast = digit_square_sum(fast)
            fast = digit_square_sum(fast)
        return slow == 1

def digit_square_sum(num):
  """This function returns the sum of the squares of the digits in a
  given number.

  Time Complexity: O(log(num))
  Space Complexity: O(1)
  """
  result = 0
  while num > 0:
    result += (num % 10)**2
    num /= 10
  return result
```


[1]: https://leetcode.com/problems/happy-number/description/
[2]: https://leetcode.com/problems/happy-number/discuss/
