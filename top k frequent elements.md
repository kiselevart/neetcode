given an int array nums and an int k, return the k most frequent elements.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2
**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1
**Output:** [1]

thoughts
create a hashmap that counts the occurence of each element

	dictionary = {}
	for i in nums:
		 dictionary[nums[i]] = dictionary.get(nums[i], 0) + 1

sort the dictionary using by value using sorted(d, key = d.get, reverse = True)
makes the dictionary sort by the max occurences first

create empty list and append the k most commonly occuring values to it
return list

Full code:

    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
	countDict = {}
	for i in nums:
	    countDict[i] = countDict.get(i, 0) + 1
			
	countDict = sorted(countDict, key=countDict.get, reverse = True)
	listK = []
	for counter, i in enumerate(countDict):
	    if counter < k:
		listK.append(i)
	return listK
