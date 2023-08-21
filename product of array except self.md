Given an integer array `nums`, return _an array_ `answer` _such that_ `answer[i]` _is equal to the product of all the elements of_ `nums` _except_ `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

**Input:** nums = [1,2,3,4]
**Output:** [24,12,8,6]

**Example 2:**

**Input:** nums = [-1,1,0,-3,3]
	**Output:** [0,0,9,0,0]

**initial thoughts**
i feel like there is some sort of math trick i am missing
this would be very simple to do if the division operator worked

also, the line about guaranteed to fit in a 32-bit integer is suspicious, maybe there is something to do with that. im also not sure what the part about the prefix and suffix means

maybe you could just bypass the division operator somehow, but use a similar method

to multiply the entire array together you must loop through it, no shortcut here as far as i can see.

	total = 1
	for i in nums:
		total = total * i

that would store the total of the whole array
can i do something with that though
cant use division so probably not

thinking about how i could use a hashmap to help, but cant come up with anything. going to look at the solution, as ive been thinking for a while without any success.

**solution**
create prefix and postfix arrays
for each position in the prefix array, the value is multiplied by the product of all values before it
the postfix does the same but starting from the back
before the prefix and after the postfix, add a 1

in the output array, multiply the 0th prefix element and the 2nd postfix element to get the answer, then 1st and 3rd and so on, youre basically skipping over the position inbetween them, which is the 1st, or in this case ith value. 

to get the 0(1) space complexity solution you are basically cheesing the fact that the output array does not count as used space, so you store the prefix in the output array, and multiply it by the calculated postfix at each position. 

**final code**
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        res = [1] * len(nums)

        prefix = 1
        for i in range(len(nums)):
            res[i] = prefix
            prefix *= nums[i]
        
        postfix = 1
        for i in range(len(nums) -1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]

        return res
```

**thoughts on problem**
i think this problem sucks. the pre-postfix thing seems to be practically impossible to come up with based on intuition, you must have taken some sort of algorithm or math class before where this sort of thing has shown up. sure there may be some geniuses that come up with this based on their intuition, but in my opinion this is way too difficult to solve intuitively. had to listen to the video explanation and focus very hard on comprehending it. furthermore, the solution with o(1) space complexity is just cheesy, as you are abusing the fact that the return array does not count as space. it is clever of course, but very unintuitive for a relative beginner like me.