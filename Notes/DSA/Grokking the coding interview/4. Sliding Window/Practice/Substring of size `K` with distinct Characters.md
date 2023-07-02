[Leetcode](https://leetcode.com/problems/substrings-of-size-three-with-distinct-characters/)

```java
class Solution {
    public int countGoodSubstrings(String s) {

        int k=3;
        int count = 0; 
        int left = 0;
        Map<Character,Integer> map = new HashMap<>();


        for(int right = 0; right< s.length(); right++){
	        //Taking element at right into window
            char ch = s.charAt(right);
            map.put(ch, map.getOrDefault(ch,0)+1);

            if(right>=k-1){
	            //Some operation
                if(map.size()==k) count++;
				
				//Removing left element from window 
				//And Moving the left pointer
                char leftch = s.charAt(left);
                map.put(leftch, map.get(leftch)-1);
                if(map.get(leftch)==0) map.remove(leftch);
                left++;
            }

        }


        return count;
    }
}

```