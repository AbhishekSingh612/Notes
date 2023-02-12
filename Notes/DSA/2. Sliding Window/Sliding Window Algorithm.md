The sliding window algorithm is a technique used to perform a particular task on a list or array. The task is to continuously slide a window of fixed length over the list/array and perform a specific operation on each window, 
- Usually Question will give an array or string and ask 
	1. To find some sub-array or substring of size K with some condition
	2. Longest or smallest sub-array or substring with some condition


## Basic template 
```java
int left = 0;

for(int right=0; right < arr.length; right++) {
// while(right < length) also possible with right++ in the end of loop

	taking element at right into window

	// while is used to shrink
	// if is used to slide
	while or if ( condition related to window size){
		some operation
		moving left pointer;
	}
}

```

#### Types
1. Fixed size window k
	- operations are done inside inner if or while before moving the left pointer as shown above (so that first window grows to size K then operations start)
2. Variable size window 
	- Operations can be done outside of inner if or while 

## Problems: 

- [x] [[1. Max Sum Subarray]]
- [x] [[2. Minimum size subarray sum]]
- [x] [[3. Longest substring with at most k distinct characters]]
- [x] [[4. Fruit into baskets]]
- [x] [[5. Longest substring without repeating characters ]]
- [x] [[6. Longest repeating character replacement ]]
- [x] [[7. Max consecutive ones iii]]
- [x] [[8. Permutation in string]]
- [x] [[9. Find all anagrams in a String]]
- [x] [[10. Minimum window substring ]]
- [x] [[11. Substring with Concatenation of All Words]]