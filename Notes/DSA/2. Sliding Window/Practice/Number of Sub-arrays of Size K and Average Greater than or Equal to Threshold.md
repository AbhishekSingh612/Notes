[Leetcode](https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold)

## Notes:
- Instead of checking average I have used min required sum for easier calculation
- Window whose sum is Greater than or Equal to required sum is valid hence count++

```java
public int numOfSubarrays(int[] arr, int k, int threshold) {
	int left = 0;
	int count = 0;

	long requiredSum = k*threshold;
	long windowSum = 0;

	for(int right = 0; right<arr.length; right++){
		windowSum += arr[right];
	   
		if(right>=k-1){
			
			if(windowSum>=requiredSum)
				count++;

			windowSum -= arr[left];
			left++;
		}

	}
	 
	return count;
}
```