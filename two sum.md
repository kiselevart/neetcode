Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

**Example 1:**

**Input:** nums = [2,7,11,15], target = 9
**Output:** [0,1]
**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

**Example 2:**

**Input:** nums = [3,2,4], target = 6
**Output:** [1,2]

**Example 3:**

**Input:** nums = [3,3], target = 6
**Output:** [0,1]

initial thoughts
probably using a hashmap 
remove the values that are larger than the target for efficiency
could look for the complement of the current value

code

	class Solution:
	    def twoSum(self, nums: List[int], target: int) -> List[int]:
	        prevMap = {}
	        for i, n in enumerate(nums):
	            diff = target - n
	            if diff in prevMap:
	                return [prevMap[diff], i]
	            prevMap[n] = i
	        return

code explanation

creating an empty dict that stores the previously accessed elements
loop through the array of numbers
see the difference between target and current value, thats what we are looking for
if the difference is in the hashmap then just return it and the index of the current value
add the current value into the hashmap, with the key being the value, and the index being the value(reversed) since we need to know the index of each entry
