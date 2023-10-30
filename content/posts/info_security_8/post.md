---
author: "Minh T. Nguyen"
title: "Random Bit Generation and Stream Ciphers"
date: "2023-10-09"
description: ""
tags: ["cybersecurity", "long-read"]
categories: ["information security"]
series: ["Information Security"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (10/09/2023):</strong> Post started!</p>

## Principles of Pseudorandom Number Generation
### Random Number
A	number	of	network	security	algorithms	and	protocols based	on	cryptography	make	use	of	random	binary	numbers:	
- Key	distribution	and	reciprocal	authentication	schemes.
- Session	key	generation.	
- Generation	of	keys	for	the	RSA	public-key	encryption	algorithm..
- Generation	of	a	bit	stream	for	symmetric	stream	encryption.

There	are	two	distinct	requirements	for	a	sequence	of	random	numbers: Randomness	and Unpredictability.

### Randomness	
The	generation	of	a	sequence	of	allegedly	random	numbers	being	random	in	some	well-defined	statistical	sense	has	been	a	concern.
- Uniform	distribution: The	frequency	of	occurrence	of	ones	and	zeros	should
be	approximately	equal.
- Independence: No	one	subsequence	in	the	sequence	can	be	inferred from	the	others

### Unpredictability	
The	requirement	is	not	just	that	the	sequence	of	numbers	be	statistically	random,	but	that	the	successive	members	of	the	sequence	are	unpredictable.

With	“true”	random	sequences	each	number	is	statistically	independent	of	other	numbers	in	the	sequence	and	therefore	unpredictable.
- True	random	numbers	have	their	limitations,	such	as	inefficiency,	so	it	is	more common	to	implement	algorithms	that	generate	sequences	of	numbers	that	appear	to	be	random.
- Care	must	be	taken	that	an	opponent	not	be	able	to	predict	future	elements	of	the	sequence	on	the	basis	of	earlier	elements.

### Pseudorandom Number
Cryptographic	applications	typically	make	use	of	algorithmic	techniques	for	random	number	generation. These	algorithms	are	deterministic	and	therefore	produce	sequences	of	numbers	that	are	not	statistically	random. If	the	algorithm	is	good,	the	resulting	sequences	will	pass	many	tests	of	randomness	and	are	referred	to	as	*pseudorandom	numbers*.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_8/imgs/random_num.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Random and Pseudorandom Number Generators.
</figcaption>
<br/>

### True	Random	Number	Generator	(TRNG)
Takes	as	input	a	source	that	is	effectively	random.

The	source	is	referred	to	as	an	entropy	source	and	is	drawn	from	the	physical	environment	of	the	computer.
- Includes	things	such	as	keystroke	timing	patterns,	disk	electrical	activity,	mouse	movements,	and	instantaneous	values	of	the	system	clock.
- The	source,	or	combination	of	sources,	serve	as	input	to	an	algorithm	that	produces	random	binary	output.

The	TRNG	may	simply	involve	conversion	of	an	analog	source	to	a	binary	output.

The	TRNG	may	involve	additional	processing	to	overcome	any	bias	in	the	source.

### Pseudorandom	Number	Generator	(PRNG)
Takes	as	input	a	fixed	value,	called the	seed,	and	produces	a	sequence	of	output	bits	using	a	 deterministic	algorithm. Quite	often	the	seed	is generated	by	a	TRNG.

The	output	bit	stream	is	determined	solely	by	the	input	value	or	values,	so	an	adversary	who	knows	the	algorithm	and	the	seed	can	reproduce	the	entire	bit	stream.

Other	than	the	number	of	bits produced	there	is	no	difference	between	a	PRNG	and	a	PRF.	

Two different forms of PRNG:
- Pseudorandom	number	generator: An	algorithm	that	is	used	to	produce	an	open-ended	sequence	of	bits. Input	to	a	symmetric	stream	cipher	is	a	common	application	 for	an	open-ended	sequence	of	bits.
- Pseudorandom	function	(PRF): Used	to	produce	a	pseudorandom	string	of	bits	of	some	fixed	length. Examples	are	symmetric	encryption	keys	and	nonces.

### PRNG	Requirements	
The	basic	requirement	when	a	PRNG	or	PRF	is	used	for	a	cryptographic	application	is	that	an	adversary	who	does	not	know	the	seed	is	unable	to	determine	the	pseudorandom	string.

The	requirement	for	secrecy	of	the	output	of	a	PRNG	or	PRF	leads	to	specific	requirements	in	the	areas	of:	
- Randomness.	
- Unpredictability.	
- Characteristics	of	the	seed.	

### Randomness	
The	generated	bit	stream	needs	to	appear	random	even	though	it	is	deterministic.

There	is	no	single	test	that	can	determine	if	a	PRNG	generates	numbers	that	have	the	characteristic	of	randomness.	If	the	PRNG	exhibits	randomness	on	the	basis	of	multiple	tests,	then	it	can	be	assumed	to	satisfy	the	randomness	
requirement.

NIST	SP	800-22	specifies	that	the	tests	should	seek	to	establish	three	characteristics:	
- Uniformity.
- Scalability.	
- Consistency.	

**Randomness	Tests**: 
- Frequency	test: The	most	basic	test	and	must	be	included	in	any	test	suite. Purpose	is	to	determine	whether	the	number	of	ones and	zeros	in	a	sequence	is	approximately	the same	as	would	be	expected	for	a	truly	random	sequence.
- Runs	test: Focus	of	this	test	is	the	total	number	of	runs	in	the	sequence,	
where	a	run	is	an	uninterrupted	sequence	of	identical	bits	bounded	before	and	after	with	a	bit	of	the	opposite	value. Purpose	is	to	determine	whether the	number	of	runs	of	ones	and	zeros	of	various	lengths	is	as	expected	for	a	random	sequence.
- Maurer’s	universal	statistical	test: Focus	is	the	number	of	bits	between	
matching	patterns. Purpose	is	to	detect	whether	or	not	the	sequence	can	be	significantly	compressed	without	loss	of	information. A	significantly compressible	sequence	is	considered	to	be	non-random.	

### Unpredictability	
A	stream	of	pseudorandom	numbers	should	exhibit	two	forms	of	unpredictability:	
- Forward	unpredictability: If	the	seed	is	unknown,	the	next	output	bit	in	the	sequence	should	be	unpredictable	in	spite	of	any	knowledge	of	previous	bits	in	the	
sequence.
- Backward	unpredictability: It	should	not	be	feasible	to	determine	the	seed	from	knowledge	of	any	generated	values.	No	correlation	between	a	seed	and	any	value	generated	from	that	seed	should	be	evident. Each	element	of	the	sequence	should	appear	to	be	the	outcome	of	an	independent	random	event	whose	probability	is	1/2.	

The	same	set	of	tests	for	randomness	also	provides	a	test	of	unpredictability.	A	random	sequence	will	have	no	correlation	with	a	fixed	value	(the	seed).

### Seed	Requirements	
The	seed	that	serves	as	input	to	the	PRNG	must	be	secure	and	unpredictable. The	seed	itself	must	be	a	random	or	pseudorandom	number. Typically	the	seed	is	generated	by	TRNG.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_8/imgs/gsi.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Generation of Seed Input to PRNG.
</figcaption>
<br/>

### Algorithm	Design	
Algorithms	fall	into	two	categories:
- Purpose-built	algorithms: Algorithms	designed	specifically	and	solely	for	the	purpose	of	generating	pseudorandom	bit	streams.
- Algorithms	based	on	existing	cryptographic	algorithms: Have	the	effect	of	randomizing	input	data.

Three	broad	categories	of	cryptographic	algorithms	are	commonly	used	to	create	PRNGs:
- Symmetric	block	ciphers.
- Hash	functions.
- Message	authentication	codes.

## Pseudorandom Number Generators
### Linear Congruential Generator

An algorithm first proposed by Lehmer that is parameterized with four numbers:
- `m`: the modulus
  - Condition: `m > 0`
- `a`: the multiplier
  - Condition: `0 < a < m`
- `c`: the increment
  - Condition: `0 ≤ c < m`
- `X₀`: the starting value, or seed
  - Condition: `0 ≤ X₀ < m`

The sequence of random numbers `{Xₙ}` is obtained via the following iterative equation:
- `Xₙ₊₁ = (aXₙ + c) mod m`.

If `m`, `a`, `c`, and `X₀` are integers, this technique will produce a sequence of integers with each integer in the range `0 ≤ Xₙ < m`.

The selection of values for `a`, `c`, and `m` is critical in developing a good random number generator:
- Generates a full-period.
- Generated sequence should appear random.
- Efficient implementation with 32-bit arithmetic.

### Blum Blum Shub (BBS) Generator

Has perhaps the strongest public proof of its cryptographic strength of any purpose-built algorithm.

Referred to as a cryptographically secure pseudorandom bit generator (CSPRBG):
- A CSPRBG is defined as one that passes the next-bit-test if there is not a polynomial-time algorithm that, on input of the first `k` bits of an output sequence, can predict the `(k + 1)st` bit with probability significantly greater than `0.5`.

**BBS	Generator**: The	security	of	BBS	is	based	on	the	difficulty	of	factoring	n.
- Choose two	large	prime	numbers	`p`	and	`q`: `p	≡	q	≡	3	(mod	4)`.
- Let	`n	=	p	×	q`.
- Choose	a	random	number	`s`,	such	that	`s`	is	relatively	prime	to	`n`.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_8/imgs/bbs.png" />
</center>
<figcaption class="img_footer">
    Fig. 3: Blum Blum Shub Block Diagram.
</figcaption>
<br/>

## Pseudorandom Number Generation Using a Block Cipher
Two	approaches	that	use	a	block	cipher	to	build	a	PNRG	have	gained	widespread
acceptance:
- **CTR	mode**: Recommended	in	NIST	SP	800-90,	ANSI	standard	X.82,	and	RFC	4086.
- **OFB	mode**: Recommended	in	X9.82	and	RFC	4086.

## Stream	Cipher	Design	Considerations
**The	encryption	sequence	should	have	a	large	period**: A	pseudorandom	number	generator	uses	a	function	that	produces	a	deterministic	stream	of	bits	that	eventually repeats; the	longer	the	period	of	repeat	the	more	difficult	it	will	be	to	do	
cryptanalysis.

**The	keystream	should	approximate	the	properties	of	a	true	random	number	stream	as	close	as	possible**:	There	should	be	an	approximately	equal	number	of	1s	and	0s. If	the	keystream	is	treated	as	a	stream	of	bytes,	then	all	of	the	256	possible	byte	values	should	appear	approximately	equally	often.

**A	key	length	of	at	least	128	bits	is	desirable**: The	output	of	the	pseudorandom	number	generator	is	conditioned	on	the	value	of	the	input	key. The	same considerations	that	apply	to	block	ciphers	are	valid.

**With	a	properly	designed	pseudorandom	number	generator	a	stream	cipher	can	be	as	secure	as	a	block	cipher	of	comparable	key	length**: A	potential	advantage	is	that	stream	ciphers	that	do	not	use	block	ciphers	as	a	building	block	are	typically	faster	and	use	far	less code	than	block	ciphers.

## RC4
Designed	in	1987	by	Ron	Rivest	for	RSA	Security. Variable	key	size	stream	cipher	with	byte-oriented	operations. Based	on	the	use	of	a	random	permutation. Eight	to	sixteen	machine	operations	are	required	per	output	byte	and	the	cipher	can	be	expected	to	run	very	quickly	in	software. RC4	is	used	in	the	WiFi	Protected	Access	(WPA)	protocol	that	are	part	of	the	IEEE	802.11	wireless	LAN	standard.	It	is	optional	for	use	in	Secure	Shell	(SSH)	and	Kerberos. RC4	was	kept	as	a	trade	secret	by	RSA	Security	until	September	1994	when the	RC4	algorithm	was	anonymously	posted	on	the	Internet	on	the	Cypherpunks	anonymous	remailers	list.

### Strength	of	RC4	
- A fundamental vulnerability was revealed in the RC4 key scheduling algorithm that reduces the amount of effort to discover the key.
- Recent cryptanalysis results exploit biases in the RC4 keystream to recover repeatedly encrypted plaintexts.
- As a result of the discovered weaknesses the IETF issued RFC 7465 prohibiting the use of RC4 in TLS.
- In its latest TLS guidelines, NIST also prohibited the use of RC4 for government use.

## Stream Ciphers Using Feedback Shift Registers
With	the	increasing	use	of	highly	constrained	devices	there	has	been	increasing	interest	in	developing	new	stream	ciphers	that	take	up	minimal	memory,	are	highly	efficient,	and	have	minimal	power	consumption	requirements. Most	of	the	recently	developed	stream	ciphers	are	based	on	the	use	of	feedback	shift	registers	(FSRs).

FSRs	exhibit	the	desired	performance	behavior,	are	well-suited	to	compact	hardware	implementation,	and	there	are	well-developed	theoretical	results	on	the	statistical properties	of	the	bit	sequences	they	produce.
- An	FSR	consists	of	a	sequence	of	1-bit	memory	cells.
- Each	cell	has	an	output	line,	which	indicates	the	value	currently	stored,	and	an	input	line.
- At	discrete	time	instants,	known	as	clock	times,	the	value	in	each	storage	device	is	replaced	by	the	value	indicated	by	its	input	line.
- The	effect	is	as	follows:	The	rightmost	(least	significant)	bit	is	shifted	out	as the	output	bit	for	this	clock	cycle;	the	other	bits	are	shifted	one	bit	position	to	the	right;	the	new	leftmost	(most	significant)	bit	is	calculated	as	a	function	of	the	other	bits	in	the	FSR.

### Grain-128a	
Grain	is	a	family	of	hardware-efficient	stream	ciphers. Grain	was	accepted	as	part	of	the	eSTREAM	effort	to	approve	a	number	of	new	stream	ciphers. The	eSTREAM	specification,	called	Grain	v1,	defines	two	stream	ciphers,	one	with	an	80-bit	key	and	a	64-bit	initialization	vector	(IV),	and	one	with	a	128-bit	key	and	80-bit	IV.	Grain	has	since	been	revised	and	expanded	to	include	authentication,	referred	to	as	Grain-128a. The	eSTREAM	final	report	states	that	Grain	has	pushed	the	state	of	the	art	in	terms	of	compact	implementation.

Grain-128a	consists	of	two	shift	registers,	one	with	linear	feedback	and	the	second	with	nonlinear	feedback,	and	a	filter	function. The	registers	are	couple	by	very	lightweight,	but	judiciously	chosen	Boolean	functions. The	LFSR	guarantees	a	minimum	period	for	the	keystream,	and	it	also	provides	balance	in	the	output.	The	NFSR,	together	with	a	nonlinear	filter,	introduces	nonlinearity	to	the	cipher. The	input	to	the	NFSR	is	masked	with	the	output	of	the	LFSR	so	that	the	state	of	the	NFSR	is	balanced.

## True Random Number Generators
### Entropy	Sources	
A	true	random	number	generator	(TRNG)	uses	a	nondeterministic	source	to	produce	randomness. Most	operate	by	measuring	unpredictable	natural	processes	such	as	pulse	detectors	of	ionizing	radiation	events,	gas	discharge	tubes,	and	leaky	capacitors. Intel	has	developed	a	commercially	available	chip	that	samples	thermal	noise	by	amplifying	the	voltage	measured	across	undriven	resistors. 

LavaRnd	is	an	open	source	project	for	creating	truly	random	numbers	using	inexpensive	cameras,	open	source	code,	and	inexpensive	hardware. The	system	uses	a	saturated	CCD	in	a	light-tight	can	as	a	chaotic	source	to	produce	the	seed;	software	processes	the	result	into	truly	random	numbers	in	a	variety	of	formats.

### Possible	Sources	of	Randomness	
RFC 4086 lists the following possible sources of randomness that can be used on a computer to generate true random sequences:
- Sound/Video Input:
  - The input from a sound digitizer with no source plugged in or from a camera with the lens cap on is essentially thermal noise.
  - If the system has enough gain to detect anything, such input can provide reasonable high-quality random bits.
- Disk Drives
  - Have small random fluctuations in their rotational speed due to chaotic air turbulence.
  - The addition of low-level disk seek-time instrumentation produces a series of measurements that contain this randomness.

**Note**: There is also an online service (random.org) which can deliver random sequences securely over the Internet.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_8/imgs/prng_vs_trng.png" />
</center>
<figcaption class="img_footer">
    Fig. 4: Comparison	of	PRNGs	and	TRNGs.
</figcaption>
<br/>

### Conditioning
A TRNG may produce an output that is biased in some way (such as having more ones than zeros or vice versa)
  
**Biased**: NIST SP 800-90B defines a random process as *biased* with respect to an assumed discrete set of potential outcomes if some of those outcomes have a greater probability of occurring than do others

**Entropy rate**:
- NIST 800-90B defines entropy rate as the rate at which a digitized noise source provides entropy.
- Is a measure of the randomness or unpredictability of a bit string.
- Will be a value between 0 (no entropy) and 1 (full entropy).

**Conditioning algorithms/deskewing algorithms**: Methods of modifying a bit stream to further randomize the bits.

**Typical conditioning methods**: is done by using a cryptographic algorithm to scramble the random bits so as to eliminate bias and increase entropy. The two most common approaches are the use of a hash function or a symmetric block cipher.

### Hash	Function	
A hash function produces an n-bit output from an input of arbitrary length

A simple way to use a hash function for conditioning is as follows:
- Blocks of m input bits, with m ≥ n, are passed through the hash function and the n output bits are used as random bits
- To generate a stream of random bits, successive input blocks pass through the hash function to produce successive hashed output blocks

### Health	Tests	on	the	Noise	Source
The	nature	of	the	health	testing	of	the	noise	source depends	strongly	on	the	technology	used	to	produce	noise.

In	general,	the	assumption	can	be	made	that	the	digitized	output	of	the	noise	source	will	exhibit	some	bias. Thus,	traditional	statistical	tests	are	not	useful	for	monitoring	the	noise	source,	because	the	noise	source	is	likely	to	always	fail. The	tests	on	the	noise	source	need	to	be	tailored	to	the	expected	statistical	behavior	of	the	correctly	operating	noise	source. The	goal	is	not	to	determine	if	the	source	is	unbiased,	but	if	it	is	operating	as	expected.

SP 800-90B specifies that continuous tests be done on digitized samples obtained from the noise source.
- The purpose is to test for variability and to determine if the noise source is producing at the expected entropy rate.

SP 800-90B mandates the use of two tests:
- **Repetition Count Test**
  - Designed to quickly detect a catastrophic failure that causes the noise source to become “stuck” on a single output value for a long time.
  - Involves looking for consecutive identical samples.
- **Adaptive Proportion Test**
  - Designed to detect a large loss of entropy, such as might occur as a result of some physical failure or environmental change affecting the noise source.
  - The test continuously measures the local frequency of occurrence of some sample value in a sequence of noise source samples to determine if the sample occurs too frequently.


SP 800-90B specifies that health tests should also be applied to the output of the conditioning component, but does not indicate which tests to use. The purpose of the health tests on the conditioning component is to assure that the output behaves as a true random bit stream. It is reasonable to use the tests for randomness defined in SP 800-22.

### Intel Digital Random Number Generator
TRNGs have traditionally been used only for key generation and other applications where only a small number of random bits were required. This is because TRNGs have generally been inefficient with a low bit rate of random bit production.

The first commercially available TRNG that achieves bit production rates comparable with that of PRNGs is the Intel digital random number generator offered on new multicore chips since May 2012. It is implemented entirely in hardware. The entire DRNG is on the same multicore chip as the processors.

## Citation
Cited as:

<blockquote>
    <summary>Random Bit Generation and Stream Ciphers</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_8/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023rbgsc,
  title   = "Random Bit Generation and Stream Ciphers",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "October",
  url     = "https://mnguyen0226.github.io/posts/info_security_8/post/"
}
```

## References
[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Oct. 09, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_8/imgs/chicago.avif" />
</center>
<figcaption class="img_footer">
    Fig. 5: Cloud gate, Chicago, Illinois, U.S.A.</br>(Image Source: 
    <a href="https://unsplash.com/photos/cloud-gate-chicago-at-daytime-SRP5wl4Ak88" class="img_footer">Antonio Gabola @ Unsplash</a>).
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