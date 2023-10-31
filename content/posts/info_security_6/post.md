---
author: "Minh T. Nguyen"
title: "Advanced Encryption Standard"
date: "2023-09-27"
description: ""
tags: ["cybersecurity"]
categories: ["information security"]
series: ["Information Security"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (09/27/2023):</strong> Post started!</p>

## Advanced Encryption Standard (AES)
### Background
A clear replacement for DES was needed as DES have demonstrated exhaustive key search attacks. We can definitely use Triple-DES; however, it is slow with small blocks. In 1997, US NIST issued call for cipher in which 15 candidates accepted in June 1998 and 5 were shortlisted in August 1999. Rijndael was selected as the AES in October 2000 and issues as FIPS PUB 107 standard in November 2001.

### AES Requiremnets
- Secret	key	symmetric	block	cipher.		
- 128-bit	data,	128/192/256-bit	keys.		
- Stronger	&	faster	than	Triple-DES.		
- Active	life	of	20-30	years	(+	archival	use).		
- Provide	full	specification	&	design	details.		
- Both	C	&	Java	implementations.
- NIST	have	released	all	submissions	&	unclassified	analyses.

### AES Evaluation Criteria
- General	security.
- Software	&	hardware	implementation	ease.
- Implementation	attacks: Timing	attacks	and	Power	analysis.
- Flexibility	(in	en/decrypt,	keying,	other	factors)

### The AES Cipher - Rijndael
The cipher was designed	by	Rijmen-Daemen	in	Belgium. It has	128/192/256	bit	keys,	128	bit	data. It is an	iterative	rather	than	feistel	cipher. AES treats data in 4 groups of 4 bytes, and operates an entire block in every round.

AES cipher was designed to be resistant against known attacks, to have speed/code compactness on many CPUs, and to be simple.

AES processes	data	as	4	groups	of	4	bytes	(state). The	key	is	expanded	into	44/52/60	(32-bit)	words. 

AES has	10/12/14	rounds	in	which	state	undergoes:	
- byte	substitution	(one	S-box	used	on	every	byte).		
- shift	rows	(simple	permutation).		
- mix	columns	(subs	using	matrix	multiply	of	groups).		
- add	round	key	(XOR	state	with	a	portion	of	expanded	key).

AES has all	operations	can	be	combined	into	XOR	and	table	lookups	-	hence	very	fast	&	efficient.

## Finite Field Arithmetic
In the AES, all	operations are	performed	on	8-bit	bytes. The	arithmetic	operations	of	addition,	multiplication,	and	division	are	performed	over	the	finite	field	GF(2^8). A	field	is	a	set	in	which	we	can	do	addition,	subtraction, multiplication,	and	division	without	leaving	the	set. Division	is	defined	with	the	following		rule:	`a	/b	=	a	(b^-1)`. An	example	of	a	finite	field	(one	with	a	finite	number	of	
elements)	is	the	set	`Z_p`	consisting	of	all	the	integers `{0,	1,	.	.	.	.	,	p	-	1}`,	where	`p`	is	a	prime	number	and	in	which	arithmetic	is	carried	out	modulo	`p`.

If one of the operations used in the algorithm is division, then we need to work in arithmetic defined over a field. Division requires that each nonzero element have a multiplicative inverse. 

For convenience and for implementation efficiency we would like to work with integers that fit exactly into a given number of bits with no wasted bit patterns. Integers in the range `0` through `2^n - 1`, which fit into an n-bit word.

The set of such integers, `Z_n`, using modular arithmetic, is not a field. For example, the integer `2` has no multiplicative inverse in `Z_n`. That is, there is no integer `b`, such that `2b` mod `2^n = 1`.

A finite field containing `2^n` elements is referred to as `GF(2^n)`. Every polynomial in `GF(2^n)` can be represented by an `n-bit` number.

## AES Structure
Processes	the	entire	data	block	as	a	single	matrix	during	each	round	using	substitutions	and	permutation.	

The	key	that	is	provided	as	input	is	expanded	into	an	array	of	forty-four	32-bit	words,	`w[i]`.

### Four Stages
- **Substitute	bytes**	–	uses	an	S-box	to	perform	a	byte-by-byte	substitution	of	the	block.
- **ShiftRows**	–	a	simple	permutation.
- **MixColumns**	–	a	substitution	that	makes	use	of	arithmetic	over	GF(2^8).
- **AddRoundKey**	–	a	simple	bitwise	XOR	of	the	current	block	with	a	portion	of	the	expanded	key.

The	cipher	begins	and	ends	with	an	**AddRoundKey**	stage. Can	view	the	cipher	as	alternating	operations	of	XOR	encryption	(AddRoundKey)	of	a	block,	followed	by	scrambling	of	the	block	(the	other	three	stages),	followed	by	XOR	encryption,	and	so	on. Each	stage	is	easily	reversible. The	decryption	algorithm	makes	use	of	the	expanded	key	in	reverse	order,	however	the	decryption	algorithm	is	not	identical	to	the	encryption	algorithm. State	is	the	same	for	both	encryption	and	decryption. Final	round	of	both	encryption	and	decryption	consists	of	only	three	stages.

## AES Transformation Functions

### Byte	Substitution
A simple	substitution	of	each	byte; uses	one	table	of	16x16	bytes	containing	a	permutation	of	all	256	8-bit	values.	

Each	byte	of	state	is	replaced	by	byte	in row	(left	4-bits)	&	column	(right	4-bits)	e.g.,	byte	{95}	is	replaced	by	row	9	col	5	byte	which	is	the	value	{2A}.

S-box	is	constructed	using	a	defined	transformation	of	the	values	in	`GF(2^8)` designed	to	be	resistant	to	all	known	attacks.

**S-Box	Rationale**:
- The	S-box	is	designed	to	be	resistant	to	known	cryptanalytic	attacks.
- The	Rijndael	developers	sought	a	design	that	has	a	low	correlation	between	input	bits	and	output	bits	and	the	property	that	the	output	is	not	a	linear	mathematical	function	of	the	input.
- The	nonlinearity	is	due	to	the	use	of	the	multiplicative	inverse.

### Shift	Rows
A	circular	byte	shift	in	each	each:	
- 1st	row	is	unchanged.
- 2nd	row	does	1	byte	circular	shift	to	left.	
- 3rd	row	does	2	byte	circular	shift	to	left.	
- 4th	row	does	3	byte	circular	shift	to	left.	

Decrypt	does	shifts	to	right.

**Shift	Row	Rationale**:
- More	substantial	than	it	may	first	appear
- The	State,	as	well	as	the	cipher	input	and	output,	is	treated	as	an	array	of	four	4-byte	columns.
- On	encryption,	the	first	4	bytes	of	the	plaintext	are	copied	to	the	first	column	of	State,	and	so	on.
- The	round	key	is	applied	to	State	column	by	column. Thus,	a	row	shift	moves	an	individual	byte	from	one	column	to	another,	which	is	a	linear	distance	of	a	
multiple	of	4	bytes.
- Transformation	ensures	that	the	4	bytes	of	one	column	are	spread	out	to	four	different	columns.

### Mix	Columns	
Each	column	is	processed	separately. Each	byte	is	replaced	by	a	value	dependent	on	all	4	bytes	in	the	colume, effectively	a	matrix	multiplication	in	`GF(2^8)`	
using	prime	poly	`m(x)=x^8+x^4+x^3+x+1`.

**Mix	Columns	Rationale**:
- Coefficients	of	a	matrix	based	on	a	linear	code	with	maximal	distance	between	code	words	ensures	a	good	mixing	among	the	bytes	of	each	column.	
- The	mix	column	transformation	combined	with	the	shift	row	transformation	ensures	that	after	a	few	rounds	all	output	bits	depend	on	all	input	bits.	

### AddRoundKey
The	128	bits	of	State	are	bitwise	XORed	with	the	128	bits	of	the	round	key.

Operation	is	viewed	as	a columnwise	operation	between	the	4	bytes	of	a	State	column	and	one	word	of	the	round	key. Can	also	be	viewed	as	a	byte-level	operation.

**AddRoundKey Rationale**:	
- Is	as	simple	as	possible	and	affects	every	bit	of	State.
- The	complexity	of	the	round	key	expansion	plus	the	complexity	of	the	other	stages	of	AES	ensure	security.

## AES Key Expansion
Takes	as	input	a	four-word	(16	byte)	key	and	produces	a	linear	array	of	44	words	(176)	bytes. This	is	sufficient	to	provide	a	four-word	round	key	for	the	initial	AddRoundKey	stage	and	each	of	the	10	rounds	of	the	cipher.	

Key	is	copied	into	the	first	four	words	of	the	expanded	key. The	remainder	of	the	expanded	key	is	filled	in	four	words	at	a	time.	

Each	added	word	`w[i]`	depends	on	the	immediately	preceding	word,	`w[i	–	1]`,	and	the	word	four	positions	back,	`w[i	–	4]`.	In	three	out	of	four	cases	a	simple	XOR	is	used. For	a	word	whose	position	in	the	w	array	is	a	multiple	of	4`,	a	
more	complex	function	is	used.

**Key	Expansion	Rationale**
- The	Rijndael	developers	designed	the	expansion	key	algorithm	to	be	resistant	to	known	cryptanalytic	attacks.
- Inclusion	of	a	rounddependent	round constant eliminates	the	symmetry	between	the	ways	in	which	round	keys are	generated	in	different	rounds.
- The	specific	criteria	that	were	used	are:	
  - Knowledge	of	a	part	of	the	cipher	key	or round	key	does	not	enable	calculation of	many	other	round-key	bits.	
  - An	invertible	transformation. 
  - Speed	on	a	wide	range	of	processors. 
  - Usage	of	round	constants	to	eliminate	symmetries.	
  - Diffusion	of	cipher	key	differences	into	the	round	keys.	
  - Enough	nonlinearity	to	prohibit	the	full	determination	of	round	key	differences from	cipher	key	differences	only. 
  - Simplicity	of	description.

## AES Implementation
AES	decryption	cipher	is	not	identical	to	the	
encryption	cipher	
- The	sequence	of	transformations	differs	although	the	form	of	the	
key	schedules	is	the	same.	
- Has	the	disadvantage	that	two	separate	software	or	firmware	modules	are	needed	for	applications	that	require	both	encryption	and	decryption.	

Two	separate	changes	are	needed	to	bring	the	decryption	structure	in	line	with	the	encryption	structure. The	first	two	stages	of	the	decryption	round	need	to	be	interchanged. The	second	two	stages	of	the	decryption	round	need	to	be	
interchanged.

### Interchanging	InvShiftRows	and	InvSubBytes
InvShiftRows	affects	the	sequence	of	bytes	in	State	but	does	not	alter	byte	contents	and	does	not	depend	on	byte	contents	to	perform	its	transformation.

InvSubBytes	affects	the	contents	of	bytes	in	State	but	does	not	alter	byte	sequence	and	does	not	depend	on	byte	sequence	to	perform	its	transformation.

Thus,	these	two	operations	commute	and	can	be	interchanged.

### Interchanging	AddRoundKey	and	InvMixColumns
The	transformations	AddRoundKey and	InvMixColumns do	not	alter	the	sequence	of bytes	in	State.

If	we	view	the	key	as	a	sequence	of	words,	then	both	AddRoundKey and	InvMixColumns operate	on	State	one	column	at	a time.

These	two	operations	are	linear	with	respect	to	the	column	input.	

### Implementation	Aspects
AES	can	be	implemented	very	efficiently	on	an	8-bit	processor. AddRoundKey	is	a	bytewise	XOR	operation. ShiftRows	is	a	simple	byte-shifting	operation. SubBytes	operates	at	the	byte	level	and	only	requires	a	table	of	256	bytes.	MixColumns	requires	matrix	multiplication	in	the	field	GF(28),	which	means	that	all	operations	are	carried	out	on	bytes.

Can	efficiently	implement	on	a	32-bit	processor:
- Redefine	steps	to	use	32-bit	words.	
- Can	precompute	4	tables	of	256-words.	
- Then	each	column	in	each	round	can	be	computed	using	4	table	lookups	+	4	XORs.	
- At	a	cost	of	4Kb	to	store	tables.

Designers	believe	this	very	efficient	implementation	was	a	key	factor	in	its	selection	as	the	AES	cipher.

## Citation
Cited as:

<blockquote>
    <summary>Advanced Encryption Standard</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_6/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023aes,
  title   = "Advanced Encryption Standard",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "September",
  url     = "https://mnguyen0226.github.io/posts/info_security_6/post/"
}
```

## References
[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Sept. 27, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_6/imgs/hawaii.avif" />
</center>
<figcaption class="img_footer">
    Fig. 1: Northern Beach, Hawaii, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/people-swimming-near-shore-with-waves-during-daytime-nlyWZtWTzCo" class="img_footer">
Luke McKeown @ Unsplash</a>).
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