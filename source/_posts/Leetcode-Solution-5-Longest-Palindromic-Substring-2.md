---
title: 5. Longest Palindromic Substring Part 2
date: 2017-11-17 20:15:01
categories: Leetcode Solution
tags:
	- String Process
	- Manacher’s Algorithm
---

In the previous article [Longest Palindromic Substring](/2017/11/06/Leetcode-Solution-5-Longest-Palindromic-Substring/), I have discussed two solutions. Although O(n^2) is an acceptable time complexity, I read some articles introducing an amazing algorithm called Manacher’s Algorithm which only has a time complexity of O(n).

In essense, this algorithm takes advantage of the symmetric property, which is a very graceful property and can be used to decrease the recalculation. Another interesting thing in this algorithm is that it adds special char such as '#' into the string. After transition, the new string is always odd so that we do not need to consider the even length condition.

		abcdefg   => #a#b#c#d#e#f#g
		abcdefgh => #a#b#c#d#e#f#g#h#

Then, this algorithm defines a function p[i] which means the max length of a palindrome centers in index i. After that, we can exploit the previous p[i] to calculate p[j] ((j > i), and calculate newer index meets maximum(i + p[i]). At last, max(p[i]) is the answer.

Reference link:
> [Longest Palindromic Substring Part II](https://articles.leetcode.com/longest-palindromic-substring-part-ii/)
> [Manacher’s Algorithm O(N) 时间求字符串的最长回文子串](https://www.felix021.com/blog/read.php?2040)