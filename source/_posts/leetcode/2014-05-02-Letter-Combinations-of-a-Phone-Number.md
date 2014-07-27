---
layout: post
title: "[LeetCode 17] Letter Combinations of a Phone Number"
comments: true
category: Leetcode
tags: [  ]
---


### Question 
[link](http://oj.leetcode.com/problems/letter-combinations-of-a-phone-number/)

<div class="question-content">
            <p></p><p>Given a digit string, return all possible letter combinations that the number could represent.
</p>

<p>
A mapping of digit to letters (just like on the telephone buttons) is given below.</p>
<p><img src="http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png"></p>

<pre><b>Input:</b>Digit string "23"
<b>Output:</b> ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
</pre>

<p>
<b>Note:</b><br>
Although the above answer is in lexicographical order, your answer could be in any order you want.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">20 minutes</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__Altough this question is not difficult, IT IS VERY IMPORTANT__. The way that recuisive/non-recursive calls are handled are very frequently examed in interviewed. 

This question can be split into 2 sub-questions. 

1. __How to convert an number into a String (i.e. 2->'abc' etc.)__ There are 2 way: __math way__, or the __simple way__. I list 2 codes below, the first of which is written by me. The second piece using HashMap is most popular in other people's solutions, for example [this one](http://rafal.io/posts/leetcode-18-letter-combinations-of-a-phone-number.html). Some people also use array of string to achieve the same result. 

2. __How to implement the code__. There might be n digits, so using n nested-loops can solve the problem, but unable to code. There are 2 ways as well: __recursive method__, and __non-recursive method__. Please refer the solutions section. 

Number convert String, Math way: 


    private String getLetters(int key) {
        if (key <= 1 || key >= 10) return "";
        // key must be in the range of [2,9]
        char first = (char) ('a' + (key - 2) * 3);
        if (key >= 8) first++;
        String letters = "";
        for (int i = 0; i < 4; i++) {
            if (i == 3 && !(key == 7 || key == 9)) break;
            letters += first++;
        }
        return letters;
    }
    String letters = getLetters('3' - '0');


HashMap way(execute time is slightly higher):


    static final HashMap<Character, String> map = new HashMap<Character, String>() {
        {
            put('2', "abc");
            put('3', "def");
            put('4', "ghi");
            put('5', "jkl");
            put('6', "mno");
            put('7', "pqrs");
            put('8', "tuv");
            put('9', "wxyz");
        }
    };
    String letters = map.get('3');


### Solution

As mentioned, there are 2 ways to code. 

__Recursive method__ seems easy at first. I split the digits into head (the first digit) and tail (the rest). For example "142", the head = 1, tail = 42. Then I use nested loop to concatenate all letters for head, and all answers for tail and get the correct answer. However, __the code uses a lot of List and does not look cool__. The performance however, is the same as the other recursive method. 

__Now I will explain another (maybe better) recursive method__. Keep an array of char, and a counter. In the beginning, counter = 0, array is empty. Then fill in the first position of the array, and increate counter by 1. Do this recursively until counter reach the last digit (at this point, insert the char array into answer set). __Be very cautious about how the array is passed__. Array is pass by reference, so the array keep getting changed. There shouldn't cause any trouble if your code is correct, but keep in mind that __during recursive call, variables passed by reference is shared by all calls. This might be dangerous unless you handle it well__ (like use of counter). Otherwise, simply always create new objects like I did in the first code (2 arraylist are created in the first code, and 0 in the second code). 

I printed execution stack for second code, which gives better illustration. 


Call letterCombinations("29");

Success	time: 0.07 memory: 380224 signal:0

len = 0, one is a 
len = 1, one is a w
len = 1, one is a x
len = 1, one is a y
len = 1, one is a z
len = 0, one is b z
len = 1, one is b w
len = 1, one is b x
len = 1, one is b y
len = 1, one is b z
len = 0, one is c z
len = 1, one is c w
len = 1, one is c x
len = 1, one is c y
len = 1, one is c z


__Last, and the most important, is the non-recursive method__. This idea is very intereting. 2 list are kept, first is called ans, and second called newAns. Now get all letters for next digit, and concatenate will all current ans using nested loop. Say currently all strings in ans is length 3, then after concatenate, the length because 4, and added to newAns. When all combinations are added to newAns, newAns become a list of string of length 4. Now one digit is finished. __Before proceed to next digit, set ans = newAns, and clear newAns__. Code below. 

### My code 

The first recursive method (my code)


    public ArrayList<String> letterCombinations(String digits) {
        ArrayList<String> ans = new ArrayList<String>();
        if (digits.length() == 0) {
            ans.add("");
            return ans;
        }
        ArrayList<String> tailAns = this
                .letterCombinations(digits.substring(1));
        String headStr = this.getLetters(digits.charAt(0) - '0');
        for (char head : headStr.toCharArray()) {
            for (String tail : tailAns) 
                ans.add(head + tail);
        }
        return ans;
    }

    private String getLetters(int key) {
        if (key <= 1 || key >= 10) return "";
        char first = (char) ('a' + (key - 2) * 3);
        if (key >= 8) first++;
        String letters = "";
        for (int i = 0; i < 4; i++) {
            if (i == 3 && !(key == 7 || key == 9)) break;
            letters += first++;
        }
        return letters;
    }


Second recursive method (learnt and rewritten by me)


    public ArrayList<String> letterCombinations(String digits) {
        ArrayList<String> ans = new ArrayList<String>();
        char[] one = new char[digits.length()];
        fill(ans, one, 0, digits);
        return ans;
    }

    private void fill(ArrayList<String> ans, char[] one, int len, String digits) {
        if (len == one.length) {
            ans.add(String.valueOf(one));
            return;
        }
        String possibleChars = getLetters(digits.charAt(0) - '0');
        for (char c: possibleChars.toCharArray()) {
            one[len] = c;
            fill(ans, one, len+1, digits.substring(1));
        }
    }

    private String getLetters(int key) {
        if (key <= 1 || key >= 10) return "";
        char first = (char) ('a' + (key - 2) * 3);
        if (key >= 8) first++;
        String letters = "";
        for (int i = 0; i < 4; i++) {
            if (i == 3 && !(key == 7 || key == 9)) break;
            letters += first++;
        }
        return letters;
    }


__The non-recursive method (learnt and rewritten by me)__

To demostrate how __HashMap__ is used, I changed the convertion method as well. 


    public ArrayList<String> letterCombinations(String digits) {
            ArrayList<String> ans = new ArrayList<String>();
            ArrayList<String> newAns = new ArrayList<String>();
            ans.add("");
            for (int i = 0; i < digits.length(); i ++) {
                String letters = map.get(digits.charAt(i));
                for (int j = 0; j < letters.length(); j ++) {
                    for (String cur: ans) {
                        newAns.add(cur + letters.charAt(j));
                    }
                }
                ans = newAns;
                newAns = new ArrayList<String>();
            }
            return ans;
    }

    static final HashMap<Character, String> map = new HashMap<Character, String>() {
        {
            put('2', "abc");
            put('3', "def");
            put('4', "ghi");
            put('5', "jkl");
            put('6', "mno");
            put('7', "pqrs");
            put('8', "tuv");
            put('9', "wxyz");
        }
    };

__Updated June 14th, rewrote the code using template__

It could have been better [writing with StringBuilder](http://answer.ninechapter.com/solutions/letter-combinations-of-a-phone-number/), but I think it's minor. 

    public List<String> letterCombinations(String digits) {
        List<String> ans = new LinkedList<String>();
        if (digits == null) {
            return ans;
        }
        String[] pad = new String[]{
            " ","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        helper(ans, "", pad, digits, 0);
        return ans;
    }
    
    private void helper(List<String> ans, String path, String[] pad, String digits, int pos) {
        if (path.length() == digits.length()) {
            ans.add(path);
            return;
        }
        String letters = pad[digits.charAt(pos) - '0'];
        for (int i = 0; i < letters.length(); i++) {
            path += letters.charAt(i) + "";
            helper(ans, path, pad, digits, pos + 1);
            path = path.substring(0, path.length() - 1);
        }
    }
