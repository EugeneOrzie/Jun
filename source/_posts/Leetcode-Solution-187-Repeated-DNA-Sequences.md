---
title: 187. Repeated DNA Sequences
date: 2017-12-10 19:42:32
categories: Leetcode Solution
tags:
	- Hash Table
	- Bit Manipulation
---

This is a great problem which covers much useful and frequent knowledge. 

If the length of a string is **n** (suppose n >= 10), then it has **n-9** kinds of 10-letter-long substrings. The problem is asking us to find all the substrings which occurs more than once. 

1. Brute Force 

	Compare all the substrings directly. Totally we need to do comparison (n-9)<sup>2</sup> times, or, to be more accurate, (n-8)*(n-9)/2 times. 
	
2. Hash Table

	Construct a Hash Table, and use it to do comparison. If we deal with hash conflict properly, the time complexity should be approximately O(n). 

	![Hash Table](/images/20171210_Hash_Table.jpg)
	
	>This image is from the Internet. If I have infringed your copyright, please contact me by email: zjisintheway@gmail.com

	In my solution, I wrote a raw **Hash Table** implementation using C programming language. It enhances my understanding of memory management and improves my recognization about the differences between different programming languages. With other high-level programming, such as **Java**, **Golang**, **php**, **python**, I just need to use the stdlib and solve this problem quickly without concerning about the allocated memory. 
	
	>Be careful: when initializing the Hash Table, each pointer of entry in the Hash Table is not always pointing to NULL(It could be anything), you should make an explicitly assignment.

	But do we need to know the details? This is a controversial problem. I do think we need to know some details and some implementations of the stdlib because this is the difference between mediocre engineers and outstanding ones. That's why I use C as my programming language when solving problems in Leetcode.

3. Bit Manipulation
	
	In my opnion, this problem is designed to let us find the features that there are only four possible different characters A, C, G, U in the string, which allows us to use 2 Bits to represent a letter. However, I think this solution is too specific with bad extensibility. What if all the characters have possibility to occur? What if the length of substrings is not just 10? 
	
	Looks like I have jealous and bitter feelings because I didn't figure out this idea during dealing with it. But I will never admit it.
		
reference:
>[Elegant and fast solution using Bit Manipulation](https://discuss.leetcode.com/topic/42092/beating-100-submission-in-c-well-explained-and-commented)

	
	