---
author: "Minh T. Nguyen"
title: "Finite Fields"
date: "2023-09-22"
description: "This post delves into the foundational structures of algebra used in information security: groups, rings, and fields."
tags: ["cybersecurity"]
categories: ["information security"]
series: ["Information Security"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (09/22/2023):</strong> Post started!</p>

## Groups
A set of elements with a binary operation denoted by “•” that associates to each ordered pair `(a,b)` of elements in `G` an element `(a • b)` in `G`, such that the following axioms are obeyed:
- **(A1) Closure**: If `a` and `b` belong to `G`, then `a • b` is also in `G`.
- **(A2) Associative**: `a • (b • c) = (a • b) • c` for all `a`, `b`, `c` in `G`.
- **(A3) Identity element**: There is an element `e` in `G` such that `a • e = e • a = a` for all `a` in `G`.
- **(A4) Inverse element:** For each `a` in `G`, there is an element `a^1` in `G` such that `a•a^1 = a^1 • a = e`.
- **(A5) Commutative (Abelian Group):** `a • b = b • a` for all `a`, `b` in `G`.


### Cyclic Group
Exponentiation is defined within a group as a repeated application of the group operator, so that `a^3 = a•a•a`.

We define `a^0 = e` as the identity element, and `a^-n = (a^1)^n`, where `a^1` is the inverse element of within the group.

A group `G` is cyclic if every element of is a power `a^k` (`k` is an integer) of a fixed element `a∈G`.

The element a is said to generate the group `G` or to be a generator of `G`.

A cyclic group is always abelian and may be finite or infinite.

## Rings
A **ring** `R` is a set with two operations: addition and multiplication.

`R` is an abelian group with respect to addition, meaning it satisfies properties like closure under addition, the existence of an identity element, and the existence of additive inverses.

Rings must also satisfy closure under multiplication, associativity of multiplication, and distributive properties of multiplication over addition.

If multiplication in a ring is commutative, the ring is said to be commutative.

An **integral domain** is a special kind of commutative ring that has a multiplicative identity and no zero divisors.

## Fields
A **field** `F` is like a ring but has additional properties.

Every non-zero element in a field has a multiplicative inverse.

Fields allow for addition, subtraction, multiplication, and division without leaving the set.

Fields have familiar examples like the rational numbers, real numbers, and complex numbers. Notably, the set of all integers is not a field because not every integer (except zero) has a multiplicative inverse.

Fields can be identifies into multiple types:
- Fields with an infinite number of elements.
- Finite fields.
  - `GF(p)` - Finite fields with `p` elements.
  - `GF(p^n)` - Finite fields with `p^n` elements.

## Relationships Between Groups, Rings, and Fields
<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_5/imgs/grf.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Groups, Rings, and Fields.
</figcaption>
<br/>

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_5/imgs/grf_properties.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Properties of Groups, Rings, and Fields.
</figcaption>
<br/>

## Finite Fields of the Form GF(p)
Finite	fields	play	a	crucial	role	in	many	cryptographic	algorithms. It	can	be	shown	that	the	order	of	a	finite	field	must	be	a	power	of	a	prime	`p^n`,	where	`n`	is	a	positive	integer.

The	finite	field	of	order	`p^n` is	generally	written	`GF(p^n)`.		

`GF`	stands	for	**Galois**	field,	in	honor	of	the	mathematician	who	first	studied	finite	fields.

**GF(p)** is defined with the following properties:
- `GF(p)` consists of `p` elements.
- The binary operations `+` and `*` are defined over the set. The operations of addition, subtraction, multiplication, and division can be performed without leaving the set. Each element of the set other than 0 has a multiplicative inverse.
- We show that the elements of `GF(p)` are the integers `0, 1, ..., p - 1` and that the arithmetic operations are addition and multiplication mod `p`.

## Polynomial Arithmetic

### Polynomial Arithmetic with Coefficients in Z_p
Division in different sets or structures can yield different results. For instance, when considering the division of 5 by 3:
- In the field of rational numbers, the result is simply the fraction `5/3`.
- In the field `Z_7`, which is the integers modulo 7, the division is expressed as `5/3 = (5 x 3^-1) mod 7`, resulting in a value of 4.
- In the ring of integers, the division produces a quotient and a remainder. In this case, `5/3` yields a quotient of 1 and a remainder of 2.

### Polynomial Division

A polynomial `f(x)` can be represented as a product of two other polynomials `a(x)` and `g(x)` plus a remainder `r(x)`. In other words: `f(x) = a(x) g(x) + r(x)`, where `r(x)` is the remainder.

If there's no remainder (i.e., `r(x) = 0`), then `g(x)` divides `f(x)` completely. This can be written as `g(x) | f(x)`.

If a polynomial `f(x)` cannot be expressed as a product of two other polynomials of lower degree over a certain field `F`, then `f(x)` is irreducible or prime over that field.

### Polynomial GCD
A polynomial `c(x)` is the greatest common divisor (GCD) of `a(x)` and `b(x)` if:
- `c(x)` divides both `a(x)` and `b(x)`.
- Any divisor of `a(x)` and `b(x)` is also a divisor of `c(x)`.

Another way to define the GCD is that it's the polynomial of the highest degree that divides both `a(x)` and `b(x)`.

The Euclidean algorithm can be extended to find the GCD of two polynomials, especially when their coefficients belong to a field.

## Finite Fields of the Form GF2^n

### Computational Considerations
Since coefficients are `0` or `1`, they can represent any such polynomial as a bit string.

Addition becomes `XOR` of these bit strings.

Multiplication is shift and XOR; cf long-hand multiplication.

Modulo reduction is done by repeatedly substituting the highest power with the remainder of the irreducible polynomial (also shift and XOR).

### Using a Generator
A generator `g` of a finite field `F` of order `q` (contains `q` elements) is an element whose first `q-1` powers generate all the nonzero elements of `F`.
- The elements of `F` consist of `0, g^0, g^1, ... , g^{q-2}`.

Consider a field `F` defined by a polynomial `f(x)`.
- An element `b` contained in `F` is called a root of the polynomial if `f(b) = 0`.

Finally, it can be shown that a root `g` of an irreducible polynomial is a generator of the finite field defined on that polynomial.

## Citation
Cited as:

<blockquote>
    <summary>Finite Fields</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_5/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023ff,
  title   = "Finite Fields",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "September",
  url     = "https://mnguyen0226.github.io/posts/info_security_5/post/"
}
```

## References
[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Sept. 22, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_5/imgs/georgia.avif" />
</center>
<figcaption class="img_footer">
    Fig. 3: Golden Gate Bridge, San Francisco, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/green-trees-near-body-of-water-during-sunset-W9ZQ3Y1Q5rw" class="img_footer">Abigail Ducote @ Unsplash</a>).
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