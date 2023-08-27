Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence

You must write an algorithm that runs in `O(n)` time.

**Example 1:**

**Input:** nums = [100,4,200,1,3,2]
**Output:** 4
**Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**

**Input:** nums = [0,3,7,2,5,8,4,6,0,1]
**Output:** 9

**Constraints:**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`

**thoughts**
* might be a good idea to first sort the array into order
* loop through the sorted array
* start a count from the first element
* if the next element is current+1 then count++
* otherwise reset the counter
* have a max var
* each time the counter resets update max var depending on the value
* return the max var after loop ends

solved it but not in O(n) since sorting is nlogn but i cant think of a better solution

**full code**
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        if not nums:
            return 0

        longest = 0
        counter = 1
        nums = list(set(nums))
        nums.sort()

        for i in range(len(nums)-1):
            if nums[i] == nums[i+1]-1:
                counter += 1
            else:
                if counter > longest:
                    longest = counter
                counter = 1

        if counter > longest:
            longest = counter
        return longest
```

**explanation**
* checks for empty list edge case
* sets longest and counter
* first turns nums into a set which removes any duplicates
* then turns it back into a list so that it can be iterable easily
* sorts the nums into order
* loops through the array, -1 in range function is to make sure it doesnt access an index out of array length
* if the following number-1 == current number add one to counter
* otherwise update longest if the counter is larger than current value, and reset counter
* on loop exit, check if counter is larger than longest again, and return the value

**neetcode solution**
* looking at sequences as if its on a number line
* identify that a sequence starts then there is no left neighbour
* convert the array into a set
* does the set contain the current value-1? 
* if not this is the start of a sequence
* is current value+1 in the set? if yes then continue
* else restart and go next element

```python 
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        numSet = set(nums)
        longest = 0
        for i in nums:
            if(i-1) not in numSet:
                length = 0
                while (i+length) in numSet:
                    length += 1
                longest = max(length, longest)
                
        return longest
```
very nice and elegant solution, helped me with my understanding of sets and time complexity