---
title: 10. 44. Regular Expression
date: 2017-11-25 21:31:53
categories: Leetcode Solution
tags:
	- Leetcode
	- Regular Expression
	- Dynamic Programming
	- Greedy Algorithm
---

## 10. Regular Expression Matching
This problem took me a long time to figure out because I went on a wrong way at first. I tried to solve it in linear time and I failed as a result, because I couldn't determine **".*"** matched which part of target string in order to have them matched. 

### Algorithm
Here is my solution utilizing Dynamic Programming.

1. Calculate the length of s and p with a for-loop, which is usually unnecessary in other language such as Java. when (p == ""), return false if (s != "") and return true if (s == "").

2. Find all the ***blocks***. The definition of blocks is better described in C language as below:

		struct block{
    		char ch;
    		bool limited;
		};
		
	b* is a block, in which block.ch = 'b' and block.limited = false.
	
	a is a block, in which block.ch = 'a' and block.limited = true.
	
	.* is a block, in which block.ch = '.' and block.limited = false.
	
	This struct is designed to express the pattern and will be used in the next step.
	
3. Suppose that f[i][j] means whether the first (i - 1)'s blocks can match the first (j-1)'s target string; f[blockLength + 1][targetStrLength + 1] is the answer.

		f[0][0] = true
		f[i][0] = true if the first (i-1)'s block.limited == false (i > 0)
		f[i][j] = f[i - 1][j - 1] if (blocks[i].limited == false && blocks[i].ch == targetStr[j]) (i > 0, j > 0)
		f[i][j] |= f[i - 1][k] if (blocks[i] matches targetStr[k+1, j]) (j >= k >= 0)
		
	annotation:
	
		blocks means the array of block.
		targetStr means the string we are going to match. targetStr[i] means the i's char. targetStr[i, j] means substring in targetStr from i to j.
		| means or.
		
### Complexity

Time complexity is O(n<sup>3</sup>). Space complexity is O(n<sup>2</sup>).

## 44. Wildcard Matching
We could reuse the solution of problem ***10. Regular Expression Matching*** to solve this problem. But after I submited my code, I found that it cost 79ms which only beated 4.88 % of other c submissions. I realized there existed a better solution immediately.

But my runtime was 9ms in previous question and beated 77.63% other c submissions. What's difference between these two questions?

It is not enough when the result is <font color=green>Accepted</font>. A better way to do the practice is to analyse it seriously and figure it out through alternative approachs in one problem other than many problems. I will work out this question in a better way in the next few days.

_______________

2017-12-07 supplement

I read some solutions from leetcode and found all of the fast solutions shared the same idea. I followed this idea and got 25ms as a result. 

This new solution has, at best, linear runtime O(m+n) and at worst, O(mn), which also has constant space complexity and short code. 

The basic idea of the solution is to have two pointers(**p** and **s**) to record the positions of target string and pattern string correspondingly. Then we could compare the chars pointed and let the two pointers advance by regulation. If the two chars are not match, then backtrack both pointers to previous recorded positions **star** and **ss**. Concrete code is listed:

	if ((*p=='?')||(*p==*s)){s++;p++;continue;} 

	if (*p=='*'){star=p++; ss=s;continue;} 
        
	if (star){ p = star+1; s=++ss;continue;} 
	

>The code above refered by [Yu's blog](https://yucoding.blogspot.com/2013/02/leetcode-question-123-wildcard-matching.html)

In fact, this solution always tried to find the substring of string **s** which equals to the string between **\*** of **p**, because **\*** in this problem could match any string. 

More specifically, we could simply regard **p** as model:

**[string]\*[string]\*[string]\*[string]...\*[string]**

If we have processed the [string] which occurs in the first and in the last(which should be easy), we just needed to match all the [string] between **\***.

Then the model changed to this:

**\*[string]\*[string]\*[string]...[string]\***

Suppose s = "abcdefabcdefg" and p = "a\*bcd\*def\*g", then let's see how this idea works. 

**Step 1**: Handle the first and last string of two strings. We can find that they both have "a" in the beginning and "g" in the last. After eliminating them, we got s' = "bcdefabcdef" and p' = "\*bcd\*def\*".

**Step 2**: Find all substrings of p' between *. We get "bcd" and "def".

**Step 3**: For each substring found in **Step 2**, find the earlist occurring position in s' and do elimination(Think about why the earlist is the best?). "bcd" occurs in the head of s', and s'' = "efabcdef". "def" occurs in the 5th index of s'', and s''' = "", and so on. Any time we can not find the substring of s, we can know that they are not match.


