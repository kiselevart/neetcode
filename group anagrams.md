given an array of strings, strs, group the anagrams together.

so if array is cat, bat, tea, eat
output will be cat, bat     tea, eat

make a hash map of strings
rough code
	
	for i in range(len(strs)):
		if strs[i].sort() in dict:
			dict[strs[i].sort()].append(strs[i]]))
		else:
			dict[strs[i].sort()] = [strs(i)]

	for i in dict:
		print(dict[i])

first leetcode problem i solved on my own!

full code:

	class Solution:
		def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
			hashArr = {}
			for i in strs:
				key = "".join(sorted(i))
				if key in hashArr:
					hashArr[key].append(i)
				else:
					hashArr[key] = [i]
			return hashArr.values()

explanation:
define empty dictionary
loop through the array of strings named strs
each i is a string from the list

create a variable named key
sorted(i) just sorts the current string
join concatenates together the string with "" as the space between the letters, as sorted creates a list of characters due to how it works

if the key is already in the dictionary, just append the current word to that array
otherwise create a new entry in the dictionary, key is the sorted word, and the value is an array with the current word in it

return all of the values in the dictionary with .values(), very useful command


