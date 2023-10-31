---
author: "Minh T. Nguyen"
title: "Number Theory"
date: "2023-08-28"
description: "Number theory is about integers and their properties. This blog post covers everything from the basics of divisibility and the Division Algorithm to advanced concepts like modular arithmetic, prime numbers, the renowned theorems of Fermat and Euler, Miller-Rabin algorithm, and the Chinese Remainder Theorem."
tags: ["cybersecurity"]
categories: ["information security"]
series: ["Information Security"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (08/21/2023):</strong> Post started!</p>

## Divibility and Division Algorithm
We say that a nonzero `b` divides a if `a = mb` for some `m`, where `a`, `b`, and `m` are integers.

**Division Algorithm**: Given any positive integer n and any non-negative integer a, if we divide a by n, we get an integer quotient q and an integer remainder r that obey the following relationship:
- `a = qn + r`
- `0	≤	r	<	n;	q	=	[a/n]`

## The Euclidean Algorithm
This is one of the basic techniques of number theory and is the procedure for determining the greatest common divisor of two positive integers.

### Greatest Common Divisor (GCD)
The greatest common divisor of a and b is the largest integer that divides both a and b, the notion is `gcd(a, b)`

Positive integer c is said to be the gcd of `a` and `b` if:
- `c` is the divisor of `a` and `b`.
- Any divisor of `a` and `b` is a divisor of `c`.

An equivalent definition is: `gcd(a,b)	=	max[k,	such	that	k	|	a	and	k	|	b]`

Because	we	require	that	the	greatest	common	divisor	be	positive,	 `gcd(a,b)	=	gcd(a,-b)	=	gcd(-a,b)	=	gcd(-a,-b)`	

In	general,	`gcd(a,b)	=	gcd(|a|,|b|)`	
- `gcd(60,	24)	=	gcd(60,	-	24)	=	12`

Also,	because	all	nonzero	integers	divide	`0`,	we	have	`gcd(a,0)	=	|a|`

We	stated	that	two	integers	a	and	b	are	relatively	prime	if	their	 only	common	positive	integer	factor	is	`1`;	this	is	equivalent	to	 saying	that	a	and	b	are	relatively	prime	if	`gcd(a,b)	=	1`
- `8`	and	`15`	are	*relatively	prime*	because	the	positive	divisors	of	`8`	are	`1`,	`2`,	`4`,	and	 `8`,	and	the	positive	divisors	of	`15`	are	`1`,	`3`,	`5`,	and	`15`.	So	`1`	is	the	only	integer	on	both	lists.	

### Euclidean Algorithm 
Two integers are *relatively prime* if their only common positive integer factor is 1.

This algorithm finds the greatest common divisor of two integers `a` and `b`.

<center>
    <img style="width: 80%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_2/imgs/euclidean_algo.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Euclidean algorithm.
</figcaption>
<br/>


Let's walk through an example:
- If	we	want	to	find	`gcd(287,	91)`,	we	divide `287`	by	`91`:				`287	=	91⋅3	+	14`.
- We	know	that	for	integers	`a`,	`b`	and	`c`,	if	`a	|	b`	and	`a	|	c,`	then	`a	|	(b	+	c)`.
- Therefore,	any	divisor	of	`287`	and	`91`	must	also	be	a	divisor	of	`287	-	91⋅3	=	14`.
- Consequently,	`gcd(287,	91)	=	gcd(14,	91)`.	
- In	the	next	step,	we	divide	`91`	by	`14`:	`91	=	14⋅6	+	7`.
- This	means	that	`gcd(14,	91)	=	gcd(14,	7)`.	
- Thus,	we	divide	`14`	by	`7`:	`14	=	7⋅2	+	0`.
- We	find	that	`7	|	14`,	and	thus	`gcd(14,	7)	=	7`.
- Therefore,	`gcd(287,	91)	=	7`.	

## Modular Arithmetic
### Modulus
If	`a`	is	an	integer	and	`n` is	a	positive	integer,	we	define	`a`	mod	`n` to	be	the	remainder	when	`a`	is divided	by	`n`;	the	integer	`n` is	called	the	modulus.

Thus,	for	any	integer	`a`:	
- `a	=	qn +	r `
- `0	≤	r	<	n;	q	=	[a/	n]`
- `a	=	[a/	n]	*		n	+	(	a	mod	n)`

Modular	arithmetic	exhibits	the	following	properties:	
- `[(a	mod	n)	+	(b	mod	n)]	mod	n =	(a	+	b)	mod	n	`
- `[(a	mod	n)	-	(b	mod	n)]	mod	n	=	(a	-	b)	mod	n`	
- `[(a	mod	n)	*	(b	mod	n)]	mod	n	=	(a	*	b)	mod	n`	

### Congruent
Two	integers	`a`	and	`b`	are	said	to	be	congruent	modulo	`n`	if: `(a	mod	n)	=	(b	mod	n)`.

This	is	written	as	`a	≡	b	(mod	n)`.

If `a	≡	0(mod	n)`,	then	`n |	a`.

Congruences	have	the	following	properties:
- `a	≡	b	(mod	n)`	if	`n	|	(a	–	b)`	(or	similarly,	`n	|	(b	–	a)`)	
- `a	≡	b	(mod	n)`	implies	`b	≡	a	(mod	n)`
- `a	≡	b	(mod	n)`	and	`b	≡	c	(mod	n)`	imply	`a	≡	c	(mod	n)`

## Prime Numbers
Prime	numbers	only have	divisors	of	1	and	itself: They	cannot	be	written	as	a	product	of	other	numbers.

Prime	numbers	are	central	to	number	theory.

## Fermat's and Euler's Theorems
### Fermat's	Theorem	
*If	`p`	is	prime	and	`a`	is	a	positive	integer	not	divisible	by	`p`	then `a^(p-1) ≡	1	(mod	p)`*.

An	alternate	form	is: *If	`p`	is	prime	and	`a`	is	a	positive	integer	then `a^p ≡ a	(mod	p)`*.

### Euler’s	Totient	Function	ϕ(n)
For	an	integer	`n`,	`ϕ(n)`		is	the	number	of	integers	`k`	in	the	range	`1	≤	k	≤	n`	for	which	the	greatest	common	divisor	`gcd(n,	k)`	is	equal	to	`1`	(`k`	is	a	relative	prime	to	`n`).

`gcd(1,1)	=	1`,	thus	`ϕ(1)	=	1`.

`ϕ(p)	=	p-1`	,	`p`	is	a	prime.

### Euler's	Theorem	
For	every	a	and	n that	are	relatively	prime: `a^(ϕ(n))	≡		1	(mod	n)`. 

An	alternative	form	is: `a^(ϕ(n)+1)	≡		a	(mod	n)`.

## Testing For Primality with Miller-Rabin Algorithm	

Typically	used	to	test	a	large	number	for	primality.

<center>
    <img style="width: 80%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_2/imgs/miller_rabin.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Miller-Rabin algorithm.
</figcaption>
<br/>

## The Chinese Remainder Theorem
*It	is	possible	to	reconstruct	integers	in	a	certain	range	from	their	residues	modulo	a	set	of	pairwise	relatively	prime	moduli*.
- This	can	be	useful	when	M	is	150	digits	or	more.
- However,	it	is	necessary	to	know	beforehand	the	factorization	of	M

The Chinese Remainder Theorem solves systems of equations of the form:
- `x ≡ a1 (mod m1)`
- `x ≡ a2 (mod m2)`
- `...` 
- `x ≡ an (mod mn)` 

When `m1`, `m2`,  and `mn` are pairwise relatively prime, there is a unique solution for `x` modulo `m1*m2*...*mn`.

Let's look at an example:
- `M1 = M/3 = 105/3 = 35`.
- `M2 = M/5 = 105/5 = 21`.
- `M3 = M/7 = 15`.
- So, `x ≡ 2 × 2 × 35 + 3 × 1 × 21 + 2 × 1 × 15 = 233 ≡ 23 (mod 105)`.
- Answer: `x ≡ 23 (mod 105)`.

## Discrete Logarithms
**Primitive	root**: For	a	prime	number	`p`,	if	`a`	is	a	primitive	root	of	`p`,	
then	`a`,	`a2`,	…,	`a(p-1)` are	distinct	`(mod	p)`.

**Discrete	Logarithms**: `b	≡ a^x (mod	p)`. The	exponent	`x`	is	referred	to	as	the	discrete logarithm	of	the	number	`b`	for	the	base	`a	(mod	p)`.		

## Citation
Cited as:

<blockquote>
    <summary>Number Theory</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_2/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023numtheory,
  title   = "Number Theory",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "August",
  url     = "https://mnguyen0226.github.io/posts/info_security_2/post/"
}
```

## References

[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Aug. 28, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_2/imgs/connecticut.avif" />
</center>
<figcaption class="img_footer">
    Fig. 3: Bulls Bridge, Kent, Connecticut U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/people-standing-in-front-of-brown-wooden-house-during-night-time-XdCpvFP-RCc" class="img_footer">Johnell Pannell @ Unsplash</a>).
</figcaption>

<!-- CSS Styling -->
<style>
.img_size {
  width: 100%;
}

.img_footer {
    color: #888888;
    text-align: center;
}
</style>