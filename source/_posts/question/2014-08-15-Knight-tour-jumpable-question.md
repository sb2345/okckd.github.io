---
layout: post
title: "[Question] 跳马问题加强版"
comments: true
category: Question
tags: [ ItInt5 ]
---

### Question 

[link](http://www.itint5.com/oj/#12)

> 有一个无限大的棋盘，棋盘上有一匹马，马可以从长宽分别为p和q的矩形一个角移动到对角。即假设马当前的位置为(x,y)，那么下一步可以移动到(x+p,y+q)，(x+p,y-q)，(x-p,y+q)，(x-p,y-q)，(x+q,y+p)，(x+q,y-p)，(x-q,y+p)或者(x-q,y-p)这8个位置。

> 问马是否能从坐标(x,y)按照上述移动规则移动到坐标(x2,y2)。

### Solution

[ref](http://www.itint5.com/discuss/16/%E8%B7%B3%E9%A9%AC%E9%97%AE%E9%A2%98%E5%8A%A0%E5%BC%BA%E7%89%88)

1. 计算dx=x-x2,dy=y-y2。
2. 求出p,q的最大公约数g，如果dx或者dy不能被g整除，那么很显然无解。
3. 将p,q,dx,dy都除以g，现在p和q互质了。
4. 注意到马可以跳到点(0,2p)（先(p,q)跳一下，然后(p,-q)跳一下），重复这个过程，马可以跳到任意(0,2kp)的点，由于对称性，也可以跳到任意(2kp,0)的点。 
5.下面这一步很关键，由于p,q互质，那么存在x,y满足px+qy=1（扩展欧几里德定理）。这样，马可以跳到(0,2)和和(2,0)，由于对称性，马可以跳到任意坐标都为偶数点。
6. 有了上面的结论，其实只用考虑(0,0),(0,1),(1,0),(1,1)这4个点是否可达。(0,0)是可达的，(0,1)和(1,0)由于对称性只用考虑(0,1)。
7. 对于(1,1)，其实是永远可达的。如果q,p都为奇数，可以先跳到(1+p,1+q)的点（利用5中的结论，可以跳到都是偶数的点），然后(-p,-q)跳到(1,1)。如果p,q一奇一偶，可以先跳到(1+p+q,1+q+p)的点（利用5中的结论），然后(-p,-q),(-q,-p)两步跳到(1,1)。
8. 对于(0,1)，如果p,q一奇一偶，那么也是永远可达的（同7可证）。如果p,q都是奇数，那么是不可能跳到(0,1)的，因为两个奇数不管怎么加减交替运算都不可能变成一奇一偶。

所以最后的结论就是：__第3步之后，如果p,q一奇一偶，那么可达。否则dx,dy同奇或同偶才可达__。

gcd的代码 (concise version):

	int gcd(int a, int b) {
		return b ? gcd(b, a % b) : a;
	}

### Code

__not written by me__

	int gcd(int a, int b){
	    return b? gcd(b, a%b) : a;
	}
	bool canJump(int p, int q, int x, int y, int x2, int y2) {
	    if(p==0 && q==0) return (x==x2)&&(y==y2);
	    int x1 = x2 - x, y1 = y2 - y;
	    int g1 = gcd(p, q);
	    if( x1 % g1 || y1 % g1) return false;
	    p = p/g1;
	    q = q/g1;
	    x1 = x1/g1;
	    y1 = y1/g1;
	    if((p-q)%2 ) return true;
	    else return (x1-y1)%2 == 0;
	}
