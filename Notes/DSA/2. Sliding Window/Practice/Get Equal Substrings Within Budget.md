
[Leetcode](https://leetcode.com/problems/get-equal-substrings-within-budget)

Notes: 
- Given two string find the longest substring which can be formed within the given maxCost where cost is difference of the ascii value of the string characters
- Variable size sliding window problem with window condition that cost should be less or equal to given maxCost

```java
public int equalSubstring(String s, String t, int maxCost) {
	int maxLen = 0;

	int left = 0; 
	int windowCost = 0;
	int len = s.length();

	for(int right = 0; right<len; right++){
		windowCost += Math.abs(s.charAt(right) - t.charAt(right));

		if(windowCost>maxCost){
			windowCost -= Math.abs(s.charAt(left) - t.charAt(left));
			left++;
		}

		maxLen = Math.max(maxLen, right - left + 1);
	}

	return maxLen;
}

```