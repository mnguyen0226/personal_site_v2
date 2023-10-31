---
author: "Minh T. Nguyen"
title: "Block Ciphers and the Data Encryption Standard"
date: "2023-09-18"
description: "In the domain of digital encryption, block ciphers play a pivotal role in securing data by converting it into ciphertexts. This article explores the mechanics of block ciphers, emphasizing the widely recognized Data Encryption Standard (DES), its structures, functions, and inherent strengths."
tags: ["cybersecurity"]
categories: ["information security"]
series: ["Information Security"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (09/18/2023):</strong> Post started!</p>

## Traditional Block Cipher Structure
### Stream Cipher
**Primary Function**: Stream Cipher encrypts a digital data stream one bit or one byte at a time.

**Examples of Stream Ciphers**: Autokeyed Vigenère cipher, Vernam cipher.

**Ideal Use-case**: In the perfect situation, a one-time pad version of the Vernam cipher would be utilized. In this scenario, the keystream length matches that of the plaintext bit stream.

**Security Consideration**: If the cryptographic keystream is entirely random, the cipher becomes impenetrable unless one obtains the keystream. To facilitate secure communication, the keystream must be shared with both users in advance using a safe and distinct channel. However, this setup can pose substantial logistical challenges, particularly when dealing with vast amounts of intended data traffic.

**Practical Implications**: The bit-stream generator should be devised using an algorithmic approach. This ensures that every involved user can reproduce the cryptographic bit stream. Predicting future parts of the bit stream based on its preceding segments should be computationally challenging.

**User Collaboration**: Both users only need to have access to the bit-stream generating method. This allows each individual to independently produce the necessary keystream.

### Block Cipher
**Functionality of Block Cipher**: A block of plaintext is processed as a unit and is converted into a ciphertext block of identical size.

**Common Block Sizes**: The typical block sizes used in block ciphers are 64 bits or 128 bits.

**Key Sharing**: Similar to the process in a stream cipher, both users involved share a symmetric encryption key.

**Prevalence in Networks**: Block ciphers dominate in network-based applications that utilize symmetric cryptographic methods.

### Feistel	Cipher
Feistel proposed the use of a cipher that alternates substitutions and permutations.

**Substitutions**: Each plaintext element or group of elements is uniquely replaced by a corresponding ciphertext element or group of elements.

**Permutation**: No elements are added or deleted or replaced in the sequence, rather the order in which the elements appear in the sequence is changed. It's a practical application of a proposal by Claude Shannon to develop a product cipher that alternates substitution and permutation functions. It's the structure used by many significant symmetric block ciphers currently in use.

**Feistel Cipher Structure** partitions the input block into two halves.
- Processes through multiple rounds.
- Performs a substitution on the left data half.
- This is based on the round function of the right half & subkey.
- Then has a permutation swapping the halves.

Feistel Cipher implements Shannon’s substitution-permutation (S-P) network concept.

**Diffusion and Confusion** was introduced by Claude Shannon to counter cryptanalysis techniques based on statistical analysis.
- Diffusion: The plaintext's statistical structure is spread into the long-range statistics of the ciphertext. Achieved by ensuring each plaintext digit impacts the value of many ciphertext digits.
- Confusion: The aim is to make the relationship between the statistics of the ciphertext and the value of the encryption key as intricate as possible. Even if an attacker can somewhat understand the ciphertext's statistics, the method by which the key generated the ciphertext is so complicated that deducing the key becomes challenging.

**Feistel Cipher Design Features**:
- Block size: Bigger block sizes yield more security but might decrease encryption/decryption speeds for a particular algorithm.
- Key size: A more significant key size offers higher security but can reduce encryption/decryption speeds.
- Number of rounds: The Feistel cipher's core idea is that one round provides inadequate security, but multiple rounds enhance security.
- Subkey generation algorithm: A more complex algorithm should result in increased difficulty for cryptanalysis.
- Round function F: Higher complexity typically indicates a higher resistance to cryptanalysis.
- Fast software encryption/decryption: In numerous scenarios, encryption is integrated into apps or utility functions in such a way that it prevents a hardware implementation; thus, the algorithm's execution speed becomes a concern.
- Ease of analysis: If an algorithm can be succinctly and clearly described, it becomes simpler to identify its cryptographic vulnerabilities and thus determine its strength with higher confidence.

## Data Encryption Standard (DES)
DES was issued	in	1977	by	the	National	Bureau	of	Standards	(now	NIST)	as	Federal	Information	Processing	Standard	46. It was	the	most	widely	used	encryption	scheme	until	the	introduction	of	the	Advanced	Encryption	Standard	
(AES)	in	2001.

The algorithm	itself	is	referred	to	as	the	Data	Encryption	Algorithm	(DEA):
- Data	are	encrypted	in	**64-bit**	blocks	using	a	**56-bit**	key.
- The	algorithm	transforms	**64-bit**	input	in	a	series	of	steps	into	a	**64-bit**	output.
- The	same	steps,	with	the	same	key,	are	used	to	reverse	the	encryption.

### DES	Round	Structure
DES round structure uses two 32-bit **L & R halves**.
  
As for any **Feistel cipher** can describe as:
- `L_i = R_(i-1)`
- `R_i = L_(i-1) xor F(R_(i-1), K)`
  
It takes 32-bit **R half** and 48-bit **subkey** and:
- Expands **R** to 48-bits using **perm E**.
- Adds to **subkey**.
- Passes through **8 S-boxes** to get 32-bit result.
- Finally permutes this using 32-bit **perm P**.

### DES	Key	Schedule	
DES key schedule forms	subkeys	used	in	each	round.

It consists	of:
- initial	permutation	of	the	key	(PC1)	which	selects	56-bits	in	two	28-bit	halves.	
- 16	stages	consisting	of:		
  - rotating	each	half	separately	either	1	or	2	places depending	on	the	key	rotation	schedule	K.	
  - permuting	them	by	PC2	for	use	in	function	f.
  - selecting	24-bits	from	each	half.

### DES	Decryption	
DES decrypt	must	unwind	steps	of	data	computation, using	subkeys	in	reverse	order	(SK16	…	SK1). Note	that	IP	undoes	final	FP	step	of	encryption.
- 1st	round	with	SK16	undoes	16th	encrypt	round.	
- ….
- 16th	round	with	SK1	undoes	1st	encrypt	round.		

Then	final	FP	undoes	initial	permutation	IP, thus	recovering	original	data	value.

### Avalanche	Effect	
- The avalanche effect is the key	desirable	property	of	encryption	algorithms, where	a	change	of	**one**	input	or	key	bit	results	in	changing	approx &&	output bits. This effect make attempts	to	“home-in”	by guessing	keys	impossible. Note, DES	exhibits	strong	avalanche.

## Strengths of DES: Timing	attacks
One	in	which	information	about	the	key	or	the	plaintext	is	obtained	by	observing	how	long	it	takes	a	given	implementation	to	perform	decryptions	on	various	ciphertexts.

DES exploits	the	fact	that	an	encryption	or	decryption	algorithm	often	takes	slightly	different	amounts	of	time	on	different	inputs.

So	far	it	appears	unlikely	that	this	technique	will	ever	be	successful	against	DES	or	more	powerful	symmetric	ciphers	such	as	triple	DES	and	AES.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_4/imgs/des.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Strength of DES with different key size.
</figcaption>
<br/>

## Block Cipher Design Principles
### Number of Rounds
- The greater the number of rounds, the more difficult it is to perform cryptanalysis.
- In general, the criterion should be that the number of rounds is chosen so that known cryptanalytic efforts require greater effort than a simple brute-force key search attack.
- If DES had 15 or fewer rounds, differential cryptanalysis would require less effort than a brute-force key search.

### Design	of	Function	F
The heart of a Feistel block cipher is the function F. The more nonlinear F, the more difficult any type of cryptanalysis will be.

The *SAC (Strict avalanche criterion)* and *BIC (Bit independence criterion)* criteria appear to strengthen the effectiveness of the confusion function. The algorithm should have good avalanche properties:
- Strict avalanche criterion (SAC): states that any output bit `j` of an S-box should change with probability 1/2 when any single input bit `i` is inverted for all `i`, `j`.
- Bit independence criterion (BIC): states that output bits `j` and `k` should change independently when any single input bit `i` is inverted for all `i`, `j`, and `k`.

### Key	Schedule	Algorithm
With	any	Feistel	block	cipher,	the	key	is	used	to	generate	one	subkey	for	each	round. In	general,	we	would	like	to	select	subkeys	to	maximize	the	difficulty	of	deducing	individual	subkeys	and	the	difficulty	of	working	back	to	the	main	key. It	is	suggested	that,	at	a	minimum,	the	key	schedule	should	guarantee	key/ciphertext	Strict	Avalanche	Criterion	and	Bit	Independence	Criterion.

## Citation
Cited as:

<blockquote>
    <summary>Block Ciphers and the Data Encryption Standard</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_4/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023des,
  title   = "Block Ciphers and the Data Encryption Standard",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "September",
  url     = "https://mnguyen0226.github.io/posts/info_security_4/post/"
}
```

## References
[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Sept. 18, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_4/imgs/florida.avif" />
</center>
<figcaption class="img_footer">
    Fig. 2: Ginnie Spring, Florida, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/green-trees-beside-body-of-water-during-daytime-jSi8CIx1XiI" class="img_footer">Autumn Kuney @ Unsplash</a>).
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