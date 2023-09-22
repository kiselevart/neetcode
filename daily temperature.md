Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ `ith` _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**

**Input:** temperatures = [73,74,75,71,69,72,76,73]
**Output:** [1,1,4,2,1,1,0,0]

**Example 2:**

**Input:** temperatures = [30,40,50,60]
**Output:** [1,1,1,0]

**Example 3:**

**Input:** temperatures = [30,60,90]
**Output:** [1,1,0]

**Constraints:**

- `1 <= temperatures.length <= 105`
- `30 <= temperatures[i] <= 100`

**thoughts**
* take a value
* loop through array
* if current value lower then append the value in the loop to the output array
* if no value is lower then append 0

**initial code**
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        ret = []
        while len(temperatures) != 0:
            curr = temperatures.pop(0)
            flag = False
            for i in range(len(temperatures)):
                if curr < temperatures[i]:
                    ret.append(i+1)
                    flag = True
                    break
            if flag == False:
                ret.append(0)
        return ret
```
this solution is too slow to pass all the testcases since its just brute force, idk how to come up with a faster solution however, so ill be looking at the posted solution video

**neetcode solution**
* 