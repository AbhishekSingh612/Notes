[Leetcode](https://leetcode.com/problems/minimum-recolors-to-get-k-consecutive-black-blocks/)

## Notes
 - Question ask to find min no of white block to paint such that we have k consecutive black blocks
 - Maintain count of W blocks in the window and keep checking their min number while sliding the window 

```java
public int minimumRecolors(String blocks, int k) {

	int min = Integer.MAX_VALUE;
	int left = 0;
	int wCount = 0;
	int bCount = 0;

	for(int right = 0; right<blocks.length(); right++){
		if(blocks.charAt(right)=='W') wCount++;

		if(right>=k-1){
			min = Math.min(min, wCount);
			
			if(blocks.charAt(left)=='W') wCount--;
			left++;
		}
	}
	return min;
}

```