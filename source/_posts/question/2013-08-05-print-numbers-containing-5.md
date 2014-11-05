---
layout: post
title: "[Question] Print Numbers containing 5"
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://www.mitbbs.com/article_t/JobHunting/32651839.html)

> 写一个function，对于参数n，输出从0到n之间所有含5的数字。eg. func(30) 应该输出5，15，25

> this is Groupon interview question

### Solution

Suggested by level 10 of [this forum](http://www.mitbbs.com/article_t/JobHunting/32651839.html). It's (surprisingly) a DFS question. 

### Code

__written by me__

	public void mySolution(int num) {
		if (num >= 5) {
			String str = String.valueOf(num);
			helper(num, "", 0, str.length(), false);
		}
	}

	private void helper(int max, String prefix, int pos, int len, boolean have5) {
		if (pos == len) {
			int cur = Integer.parseInt(prefix);
			if (cur <= max) {
				System.out.print(cur + ", ");
			}
			return;
		}
		for (int i = 0; i < 10; i++) {
			if (pos == len - 1 && !have5 && i != 5) {
				continue;
			}
			helper(max, prefix + i, pos + 1, len, have5 || i == 5);
		}
	}
