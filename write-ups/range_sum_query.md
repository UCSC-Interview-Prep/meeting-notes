# Range Sum Query - Immutable

## [Problem Statement][1]:
```
Given an integer array nums, find the sum of the elements between indices i
and j (i ≤ j), inclusive.

Note:
1) You may assume that the array does not change.
2) There are many calls to sumRange function.
```
## [Solution][2]:
```python
class NumArray(object):
    def __init__(self, nums):
        """This function initializes the num array with the prefix sum
        of a given list of ints so that later calls to sumRange run in
        O(1) time.

        Time Complexity: O(len(nums))
        Space Complexity: O(len(nums))
        """
        # Handle empty input list.
        prefix = []
        if nums:
          prefix.append(nums[0])
          for i in xrange(1, len(nums)):
            prefix.append(prefix[-1] + nums[i])
        self.prefix = prefix

    def sumRange(self, i, j):
        """This function returns the sum of the elements between indices
        i and j (i <= j), inclusive.

        Time Complexity: O(1)
        Space Complexity: O(1)
        """
        # Handle empty input list.
        if not self.prefix:
          return 0
        if i == 0:
          return self.prefix[j]

        return self.prefix[j]-self.prefix[i-1]
```


[1]: https://leetcode.com/problems/range-sum-query-immutable/description/
[2]: https://leetcode.com/problems/range-sum-query-immutable/discuss/
