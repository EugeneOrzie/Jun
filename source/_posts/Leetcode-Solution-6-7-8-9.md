---
title: 6. 7. 8. 9. Leetcode Solution
date: 2017-11-22 17:45:26
categories: Leetcode Solution
tags:
	- Leetcode
	- String Process
---

## 6. ZigZag Conversion   

Though the description is vague, this problem is not difficult. I wrote down the situation in the white paper when number is small, then found the regulation.

The most important thing is to figure out the difference (which equals to  (2 * rows - 2)). Then loop from row 0 to row row_number - 1 and print the char.

## 7. Reverse Integer   

This is a easy problem, so I don't have much to say. Just be careful about the special case.

## 8. String to Integer (atoi)   

It is interesting to implement c function **atoi**. In order to implement a function, it is important to determine the requirements. 

## 9. Palindrome Number
This question is a easy one. It could reuse the function of problem 7.