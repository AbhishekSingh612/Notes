[Leetcode](https://leetcode.com/problems/minimum-number-of-flips-to-make-the-binary-string-alternating/)

Notes: 
- Rotating the binary string usually needs concatenation with sliding window
- We can also skip concatenation by iteration 2 times the len of string and using i%len as index while accessing the character of string
- Here we are generating the valid character of the Binary string if it started with 0 or with 1 after which are counting how many flips will be needed for each in the current window
- Also after each window we are calculating the min 

```java
public int minFlips(String s) {
	int k = s.length();
	String b = s+s;
	int left = 0;

	int count0 = 0;
	int count1 = 0;

	int min = 1000_000;
	
	for(int right = 0; right<b.length(); right++){
		char curr = b.charAt(right);

		char valid0 = (right%2==0)? '0' : '1';
		char valid1 = (right%2==0)? '1' : '0';

		if(valid0!=curr)
			count0++;
		if(valid1!=curr)
			count1++;
		
		if(right>=k-1){
			min = Math.min(min, Math.min(count0,count1));

			char leftch = b.charAt(left);
			char valid0left = (left%2==0)? '0' : '1';
			char valid1left = (left%2==0)? '1' : '0';
			if(valid0left!=leftch)
				count0--;
			if(valid1left!=leftch)
				count1--;
			left++;

		}


	}

	return min;
}

```

more understandable code

```java
public int minFlips(String s) {
    int n = s.length(), res0 = 0, res1 = 0, res = n;

    for(int i = 0; i < 2 * n; i++){
        char characterInString = s.charAt(i % n);//current character
        char characterInStringStartingWith0 = i % 2 == 0 ? '0' : '1';//calculate character in 01010101..... at i
        char characterInStringStartingWith1 = i % 2 == 0 ? '1' : '0';//calculate character in 10101010..... at i

        if(characterInStringStartingWith0 != characterInString) res0++;//doesn't match means we need to flip
        if(characterInStringStartingWith1 != characterInString) res1++;//doesn't match means we need to flip
        
        if(i >= n) {//valid window
            int windowStart = i - n;//leftmost element of the window
            char characterInStringStartingWith0AtWindowStart = windowStart % 2 == 0 ? '0' : '1';//calculate character in 01010101..... at window start
            char characterInStringStartingWith1AtWindowStart = windowStart % 2 == 0 ? '1' : '0';//calculate character in 10101010..... at window start

            if(characterInStringStartingWith0AtWindowStart != s.charAt(windowStart)) res0--;//doesn't match means we flipped this before, subtract 1
            if(characterInStringStartingWith1AtWindowStart != s.charAt(windowStart)) res1--;//doesn't match means we flipped this before, subtract 1

            res = Math.min(res, Math.min(res0, res1));//calculate min 
        }
    }
    return res;
    }
```

removing new  string creation and additional valid codition

```java
public int minFlips(String s) {
	int k = s.length();
	int left = 0;

	int count0 = 0;
	int count1 = 0;

	int min = 1000_000;
	
	for(int right = 0; right<2*k; right++){
		char curr = s.charAt(right%k);

		char valid0 = (right%2==0)? '0' : '1';

		if(valid0!=curr)
			count0++;
		else
			count1++;
		
		if(right>=k-1){
			min = Math.min(min, Math.min(count0,count1));

			char leftch = s.charAt(left%k);
			char valid0left = (left%2==0)? '0' : '1';
			if(valid0left!=leftch)
				count0--;
			else
				count1--;
			left++;

		}


	}

	return min;
}

```