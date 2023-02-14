[Leetcode](https://leetcode.com/problems/maximum-average-subarray-i)

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int left=0;
        int max = Integer.MIN_VALUE;
        int windowSum = 0;

        /** for(int i=0; i<k; i++){
	    windowSum+=nums[i];
		}
		max = windowSum;

		for(int right = k; right<nums.length; right++,left++){
		    windowSum= windowSum + nums[right]-nums[left];
		    max = Math.max(max, windowSum);
		}*/

        for(int right = 0; right<nums.length; right++){
            windowSum += nums[right];

                
            if(right>=k-1){
                max = Math.max(max, windowSum);
                windowSum -= nums[left++];
            }
               
        }

        return (double)max/k;
    }
}
```

