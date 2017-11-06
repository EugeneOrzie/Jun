---
title: 5. Longest Palindromic Substring
date: 2017-11-06 16:33:47
tags: 
	- Leetcode
	- String Process
	- Dynamic Programing
categories: Leetcode Solution
---

Given a string s, find the longest palindromic substring in s，the maximum length of s is 1000.


1. Brute force

	Search the length and start, so we could calculate end by the formula: end 	= (start + length - 1). Then judge whether S[start : end] is a palindromic.
	
	Time complexity is O(n3) and space complexity is O(n), which is so terrible!
	
2. optimize

	It is obvious that we have done a lot of work which is unnecessary in Brute Force Solution. For example, for the judgement of s[i :j ] and s[i : j + 1], we loop from i to j for two times! When we judge whether s[i : j] (j - i > 1) is a palindromic string, we could easily get the result by s[i + 1: j - 1] which could also be calculated by a shorter substring, then the recursive formular appears.
	
	Assume is_ palindromic[i : j] is true when s[i : j] is a palindrome and is false vice versa. We could calculate this two-dimensional array first. 
	
		1. is_palindromic[i : j] = true; for (i == j)
		2. is_palindromic[i : j] = s[i] == s[j]; for (i + 1 == j)
		3. is_palindromic[i : j] = (is_ palindromic[i + 1: j - 1] && s[i] == s[j]); for (i + 2 <= j)
	
	Then, we just need to find is_ palindromic[i : j] is true and j - i + 1 is the largest.

	Time complexity is O(n2) and space complexity is O(n2). This result is acceptable.