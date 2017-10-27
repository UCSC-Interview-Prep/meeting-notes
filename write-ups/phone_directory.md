# Design Phone Directory

## [Problem Statement][1]:
```
Design a Phone Directory which supports the following operations:

get: Provide a number which is not assigned to anyone.
check: Check if a number is available or not.
release: Recycle or release a number.
```
## [Solution][2]:
```python
class PhoneDirectory(object):

    def __init__(self, max_nums):
        """This function initializes the phone directory.

        Time Complexity: O(max_nums)
        Space Complexity: O(max_nums)
        """
        self.is_available = [True] * max_nums
        self.available = range(max_nums-1, -1, -1)

    def get(self):
        """This function returns an unassigned phone number if one is
        available. Otherwise, this function returns -1.

        Time Complexity: O(1)
        Space Complexity: O(1)
        """
        if self.available:
            num = self.available.pop()
            self.is_available[num] = False
            return num
        return -1


    def check(self, num):
        """This function checks if a given phone number is available.

        Time Complexity: O(1)
        Space Complexity: O(1)
        """
        return self.is_available[num]


    def release(self, num):
        """This function releases a given phone number.

        Time Complexity: O(max_nums)
        Space Complexity: O(1)
        """
        if not self.is_available[num]:
            self.is_available[num] = True
            # The problem expects us to keep available phone numbers
            # in sorted order.
            i = 0
            while i < len(self.available) and num < self.available[i]:
                i += 1
            self.available.insert(i, num)
```
