[128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/description/)

```python
# 128. Longest Consecutive Sequence
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        # Variable to store the length of the longest consecutive sequence
        longest = 0

        # Convert the list to a set for O(1) average time complexity lookups
        nums_set = set(nums)

        # Iterate through each unique number in the set
        for i in nums_set:
            # Variable to count the length of the current consecutive sequence
            length = 0

            # If the previous number exists, this is not the start of a sequence
            if i - 1 in nums_set:
                continue

            # Count consecutive numbers starting from i
            while i + length in nums_set:
                length += 1

            # Update the longest sequence length found so far
            longest = max(longest, length)

        # Return the length of the longest consecutive sequence
        return longest
```
