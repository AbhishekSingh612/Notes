The sliding window algorithm is a technique used to perform a particular task on a list or array. The task is to continuously slide a window of fixed length over the list/array and perform a specific operation on each window


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

## Problems: 

- [x] [[1. Max Sum Subarray]]
- [x] [[2. Minimum size subarray sum]]
- [x] [[3. Longest substring with at most k distinct characters]]
- [x] [[4. Fruit into baskets]]
- [ ] [[5. Longest substring without repeating characters ]]
- [ ] [[6. Longest repeating character replacement ]]
- [ ] [[7. Max consecutive ones iii]]
- [ ] [[8. Permutation in string]]
- [ ] [[9. Find all anagrams in a string]]
- [ ] [[10. Minimum window substring ]]
- [ ] [[11. Substring with concatenation of all words]]