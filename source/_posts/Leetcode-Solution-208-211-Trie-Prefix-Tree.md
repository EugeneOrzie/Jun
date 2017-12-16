---
title: 208. 211. Trie(Prefix Tree) 
date: 2017-12-16 14:49:00
categories: Leetcode Solution
tags:
	- Trie
	- Prefix Tree
	- Structure Design
---

In my opinion, [**208. Implement Trie(Prefix Tree)**](https://leetcode.com/problems/implement-trie-prefix-tree/) and [**211. Add and Search Word Data structure design**](https://leetcode.com/problems/add-and-search-word-data-structure-design/description/) share the same idea: **208** is the direct implementment and **211** is the application of **Trie**.

### Introduction

Trie, also named as Prefix Tree, is a tree structure that is usually used to search for strings(or strings contains a specific prefix) very quickly. 

Basicly, The Trie is a tree and every node except root of this tree contains a char. Each node can represent a string which consists with chars contained by all nodes in the path from root sequentially. 

![Trie](/images/20171216_Trie_example.png)

### Scenerio

1. Find whether a word is in the dictionary.
2. Find all the words start with a specific prefix.
3. How many times does a word occur in a article.

> A Trie can provide an alphabetical ordering of the entries by key. -- wikipedia

### Performance

Operation| Time Complexity | Space Complexity
:-------:|:----------:|:-----:
Insert | O(h) | O(h)
Search | O(h) | NULL
Delete | O(h) | O(h)

> h is the length of word.

### Limitation

As we can see, the performance of Trie is related to the length of a string. If the average length of strings is too long (such as 1k, 1m or even more) and they have a low occurrence rate, we will build a sparse tree. Under this situation we have a bad performance. 

So, we usually call trie as *Dictionary Tree* in Chinese because all the words in the dictionary is short and similar(they share many nodes in Trie). It is fitting and proper to store the words of a dictionary by using Trie.

### Implementation
 
	struct trieNode{
		int occurTimes;
		char character;
		struct trieNode** childs;
	}
	
The Insertion and Search operation can be refered from [here][1].

Obviously, this structure is simple and useful to implement a trie, but it wastes space storing NULL pointers. The array of struct trieNode\*, **childs**, may initial n(depends on the target we need to represent) pointers pointing NULL. If the tree is sparse, then there are many NULL pointers.

One way to reduce the space waste is called *alphabet reduction*. In essence, it reduces the storage cost of one node, but makes the path longer.

[1]:https://github.com/EugeneOrzie/leetcode/blob/master/201-250/208_Implement_Trie_(Prefix_Tree).c