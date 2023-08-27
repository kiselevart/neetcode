**description**
design two functions, encode and decode.
encode transforms a list of strings into one singular string, while decode does the opposite.

**Example1**

```
Input: ["lint","code","love","you"]
Output: ["lint","code","love","you"]
Explanation:
One possible encode method is: "lint:;code:;love:;you"
```

**Example2**

```
Input: ["we", "say", ":", "yes"]
Output: ["we", "say", ":", "yes"]
Explanation:
One possible encode method is: "we:;say:;:::;yes"
```
not sure why example2 has so many colons, but ill just assume that they want a colon and a semicolon between each word when going from a list to one string

**thoughts**
* this seems to be a pretty easy problem, but maybe im wrong
* i feel like you could just use the join function here

since this is a premium question and im too lazy to sign up for lintcode i will just go through the solution

**neetcode solution**
* the problem with the encoding is that any character can be present within the string, so its difficult to know what to use as the delimiter
* put the number of characters within the string in the beginning of the string, and have a delimiter between the number and the string
* read the integer and after the delimiter read the number of characters that the integer was
* this works regardless of what happens because the string always will start with an integer, and the delimiter character following the actual delimiter will not change the fact that they are also factored into the count
* time complexity is O(n)

**full code**

```python
class Solution:
	def encode(self,strs):
		res = ""
		
		for s in strs:
			res += str(len(s)) + "#" + s #encoding the strings
		return res

	def decode(self, str):
		res, i = [], 0
		
		while i < len(str):
			j = i
			while str[j] != "#":
				j += 1
			length = int(str[i:j])
			res.append(str[j+1 : j+1+length])
			i = j+1+length
		return res

```
**code explanation**
* the encode function creates an empty return string, and loops through the array, storing each string in s
* it adds the length of each string and a delimiter (# in this case) before the string s
* after the loop ends all the strings have been combined so they are returned
* the decode function creates an empty array and a counter i set to 0
* while i is less than the total length of the entire string containing all the substrings
* j is set to i
* while the current character in j is not the delimiter character
* j is incremented 
* once we reach the delimiter we exit the while loop knowing that the integer that shows the length of the string following the delimiter ends right before j
* therefore we extract the string from i to j as the length
* convert that to int since its an integer
* extract the part of the total string starting from right after the delimiter (j+1) to the end of the substring (j+1+length) and append it to the result array
* return the array