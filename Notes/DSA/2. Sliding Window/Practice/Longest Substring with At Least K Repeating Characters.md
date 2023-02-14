
[Leetcode](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters)

Notes: 
- When trying to use sliding window here I realized there is no condition based on which I can shrink the window as we don't know whether invalid string will become valid while we expand our window 
- So I added additional condition to the window that it must contain only required number of unique character, Now we can shrink our window based on this condition 
- And In the end our result will be max of all the results we get from having 1 unique to 26 unique character 

```java
public int longestSubstring(String s, int k) {
	
	int maxLen = 0;

	// Adding additional constrain to the window so that we can 
	// shrink our window based on this condition
	for(int reqUnique = 1; reqUnique<=26; reqUnique++){

		Map<Character, Integer> map = new HashMap<>();
		int left = 0, countAtleastK = 0;

		for(int right = 0; right<s.length(); right++){
			
			//Counting the frequency of new character
			char rightCh = s.charAt(right);
			map.put(rightCh, map.getOrDefault(rightCh,0)+1);

			// Tracking number of characters in the window 
			// that appear atleast K times in our window
			if(map.get(rightCh)==k) countAtleastK++;
			
			// Shrinking the window till we have required Unique 
			// characters 
			while(map.size() > reqUnique && left<right){
				
				char leftCh = s.charAt(left);

				// Decreasing the count as after removing the leftmost 
				// character its freq will be less than K in window
				if(map.get(leftCh)==k) countAtleastK--;

				// Decreasing the Freq of the leftmost character
				map.put(leftCh, map.get(leftCh)-1);
				if(map.get(leftCh)==0) map.remove(leftCh);
				left++;
			}

			// window is valid if it has required unique character and 
			// all of them appear atleast K times
			if(map.size() == reqUnique && map.size() == countK){
				maxLen = Math.max(maxLen, right - left+1);
			}
			
		}
	}
	
	return maxLen;

}
```