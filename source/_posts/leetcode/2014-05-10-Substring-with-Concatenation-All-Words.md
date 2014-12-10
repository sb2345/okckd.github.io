---
layout: post
title: "[LeetCode 30] Substring with Concatenation of All Words"
comments: true
category: Leetcode
tags: [  ]
---

### Question 

[link](http://oj.leetcode.com/problems/substring-with-concatenation-of-all-words/)

<div class="question-content">
            <p></p><p>
You are given a string, <b>S</b>, and a list of words, <b>L</b>, that are all of the same length. Find all starting indices of substring(s) in S that is a concatenation of each word in L exactly once and without any intervening characters.
</p>

<p>
For example, given:<br>
<b>S</b>: <code>"barfoothefoobarman"</code><br>
<b>L</b>: <code>["foo", "bar"]</code>
</p>

<p>
You should return the indices: <code>[0,9]</code>.<br>
(order does not matter).
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

There are 2 ways to solve this question. __The naive approach takes around 1200ms to pass__, and __the KPM-like approach takes around half of that time__. Both methods are explained well in [this blog](http://n00tc0d3r.blogspot.sg/2013/06/substring-with-concatenation-of-all.html).

#### The HashMap

Before the solution, I will like to do a recap on __HashMap__.

<blockquote cite="http://www.sparknotes.com/cs/searching/hashtables/section1.html">
<div>
<a href="http://www.sparknotes.com/cs/searching/hashtables/section1.html">link</a>
</div>
<p>
A hash table is made up of two parts: an array (the actual table where the data to be searched is stored) and a mapping function, known as a hash function. 
</p>
<p>
The hash function is a mapping from the input space to the integer space that defines the indices of the array. In other words, the hash function provides a way for assigning numbers to the input data such that the data can then be stored at the array index corresponding to the assigned number.
</p>
</blockquote>

For example, if I want to store <"Durant">, I pass "Durant" into the hash function, and get (let's say) number 3. So in the Hash Table, it will store table(3 -> "Durant"). 

In this way, the __searching of HashMap can almost achieve  O(1) time in best case__ (like array access). 

However,

<blockquote cite="http://stackoverflow.com/a/9214421">
<div>
<a href="http://stackoverflow.com/a/9214421">link</a>
</div>
<p>
For average case, It really is (as the wikipedia page says) O(1+n/k) where K is the hash table size. If K is large enough, then the result is effectively O(1). But suppose K is 10 and N is 100. In that case each bucket will have on average 10 entries, so the search time is definitely not O(1); it is a linear search through up to 10 entries.
</p>
</blockquote>

In practise, we will just assume search in HashMap always O(1). 

Below is a great conclusion.

<blockquote cite="http://stackoverflow.com/a/9214594">
<div>
<a href="http://stackoverflow.com/a/9214594">link</a>
</div>
<p><a href="http://en.wikipedia.org/wiki/Hash_table">Hash tables</a> are <code>O(1)</code> <strong>average and <a href="http://en.wikipedia.org/wiki/Amortized_analysis">amortized</a></strong> case complexity, however is suffers from <code>O(n)</code> <strong>worst case</strong> time complexity. [And I think this is where your confusion is]</p>

<p>Hash tables suffer from <code>O(n)</code> worst time complexity due to two reasons:</p>

<ol>
<li>If too many elements were hashed into the same key: looking inside this key may take <code>O(n)</code> time.</li>
<li>Once a hash table has passed its <a href="http://en.wikipedia.org/wiki/Load_balancing_%28computing%29">load balance</a> - it has to rehash [create a new bigger table, and re-insert each element to the table]. </li>
</ol>

<p>However, it is said to be <code>O(1)</code> average and amortized case because:</p>

<ol>
<li>It is very rare that many items will be hashed to the same key [if you chose a good hash function and you don't have too big load balance.</li>
<li>The rehash operation, which is <code>O(n)</code>, can at most happen after <code>n/2</code> ops, which are all assumed <code>O(1)</code>: Thus when you sum the average time per op, you get : <code>(n*O(1) + O(n)) / n) = O(1)</code></li>
</ol>
</blockquote>

### Solution

__The naive approach uses a HashMap__. Reason 1 is because there can be duplications in L, and reason 2 is the searching is faster. 

__Time complexity of this solution is O((n - k * m) x m)__, and __space is the size of list L, O(m)__. If m is not very big, the time can be regarded as O(n). 

__some variables used in this question__.

* n - length of the input string
* L - a list of words (dictionary)
* m - the size of L
* k - the length of each word in L (all words have same length)
* (k * m) - this is the length of a possible concatenation
* (n - k * m) - this is the number of possible concatenation exist

### My code 

__Updated on July 7th__, code. 

    public List<Integer> findSubstring(String S, String[] L) {
        List<Integer> ans = new ArrayList<Integer>();
        if (S == null || L == null || S.length() == 0 || L.length == 0) {
            return ans;
        }
        HashMap<String, Integer> set = new HashMap<String, Integer>();
        for (String str: L) {
            if (set.containsKey(str)) {
                set.put(str, set.get(str) + 1);
            } else {
                set.put(str, 1);
            }
        }
        int num = L.length;
        int len = L[0].length();
        for (int i = 0; i <= S.length() - num * len; i++) {
            // start from i, check (num) words of length (len)
            HashMap<String, Integer> setCopy = new HashMap<String, Integer>(set);
            for (int j = 0; j < num; j++) {
                String cur = S.substring(i + j * len, i + (j + 1) * len);
                if (setCopy.containsKey(cur)) {
                    if (setCopy.get(cur) == 1) {
                        setCopy.remove(cur);
                    } else {
                        setCopy.put(cur, setCopy.get(cur) - 1);
                    }
                } else {
                    break;
                }
            }
            if (setCopy.isEmpty()) {
                ans.add(i);
            }
        }
        return ans;
    }
