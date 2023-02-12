[Leetcode](https://leetcode.com/problems/contains-duplicate-ii)

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        int left =0;
        // HashMap<Integer,Integer> map = new HashMap<>();

        // for(int right = 0; right<nums.length; right++){
        //     int n = nums[right]; 

        //     if(right - left > k){
        //         map.put(nums[left], map.get(nums[left])-1);
        //         if(map.get(nums[left])<=0) map.remove(nums[left]);
        //         left++;
        //     }

        //     if(map.containsKey(n)) return true;
        //     map.put(n, map.getOrDefault(n,0)+1);  
            
        // }


		//As duplicate is not allowed we can use hashset 
        Set<Integer> set = new HashSet<>();
        for(int right = 0; right<nums.length; right++){
            int n = nums[right];
            if(right>k)
                set.remove(nums[left++]);
            if(set.contains(n)) return true;
            set.add(n);
        }

        return false;
    }
}
```

