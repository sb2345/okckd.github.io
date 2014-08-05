---
layout: post
title: "[Question] Longest Substring Which Contains 2 Unique Characters"
comments: true
category: Question
tags: [ cc150 ]
---

### Question 

[link](http://www.programcreek.com/2013/02/longest-substring-which-contains-2-unique-characters/)

> Given a string, find the longest substring that contains only two unique characters. For example, given "abcbbbbcccbdddadacb", the longest substring that contains 2 unique character is "bcbbbbcccb".

### Solution

__This is a naive solution__, which we use 2 pointers and 1 hashset. The code is very readable (written by me). 

What if the question change from '2 unique chars' to 'N unique chars'? I think we can __use HashMap instead of HashSet__ (for searching of start pointer). The rest of the is very similar. 

### Code

__writen by me__

	private String solution(String input) {
		HashSet<Character> set = new HashSet<Character>();
		char[] letters = input.toCharArray();
		set.add(letters[0]);

		int start = 0;
		String longest = input.substring(0, 1);

		for (int i = 1; i < input.length(); i++) {
			if (set.add(letters[i])) {
				if (set.size() > 2) {
					// first, update the longest substring that exists before i
					if (i - start > longest.length()) {
						longest = input.substring(start, i);
					}
					// clear and rebuild the HashSet
					set.clear();
					set.add(letters[i]);
					set.add(letters[i - 1]);
					// remove 1 char entirely from current substring
					int p = i - 1;
					while (p > 0 && letters[p] == letters[p - 1]) {
						p--;
					}
					start = p;
				}
			}
		}
		if (input.length() - start > longest.length()) {
			longest = input.substring(start);
		}
		return longest;
	}
