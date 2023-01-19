# Two pointers Algorithm
The two pointers algorithm is a technique used to solve problems involving arrays or linked lists. The basic idea behind the algorithm is to use two pointers, one at the beginning of the array or list and one at the end, and to move them towards each other based on some condition
## Identifying
Ways to Identify `Two Pointers` Problem :-
1. Problem has sorted array (or Linked List) and we have to find set of elements that fulfill certain constrains
2. The set of element is a pair, triplet or sub-array
## Example
```java
int low = 0;
int high = nums.length - 1;

while (low < high) {
	int sum = nums[low] + nums[high];
	
	if (sum == target) {
	    System.out.printf("Pair found (%d, %d)", nums[low], nums[high]);
	    return;
	}
	
	else if (sum < target) {
	    low++;
	}
	
	else {
	    high--;
	}
}
```
## Questions
