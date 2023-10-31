---
author: "Minh T. Nguyen"
title: "Classical Encryption Techniques"
date: "2023-09-04"
description: "Let's dive into classical encryption techniques: from Caesar's simple shifts to more complex methods like the Playfair and Vigenère Ciphers, we'll see how each technique works and why they matter."
tags: ["cybersecurity"]
categories: ["information security"]
series: ["Information Security"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: true
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (09/04/2023):</strong> Post started!</p>

## Definitions
**Plaintext**: an original message.

**Ciphertext**: the coded message.

**Enciphering/Encryption**: the process of converting from plaintext to ciphertext.

**Deciphering/Decryption**: restoring the plaintext from the ciphertext.

**Cryptography**: the area of study of the many schemes used for encryption.

**Cryptographic System/Cipher**: a scheme.

**Cryptanalysis**: techniques used for deciphering a message without any knowledge of the enciphering details.

**Cryptology**: the areas of cryptography and cryptanalysis.

## Symmetric Cipher Model
There	are	two	requirements	for	secure	use	of	conventional	encryption:	
- A	strong	encryption	algorithm	
- Sender	and	receiver	must	have	obtained	copies of	the	secret	key	in	a	secure	fashion	and	must keep	the	key	secure. Here, the sender and receiver should get the same key.

### Cryptographic	Systems
Cryptographic	systems characterized along 3 independent dimensions:
- The type of operations used for transforming plaintext to ciphertext.
  - Substitution.
  - Transposition.
- The number of keys used.
  - Symmetric, single-key, secret-key, conventional encryption.
  - Asymmetric, two-key, or public-key encryption.
- The way in which the plaintext is processed.
  - Block cipher.
  - Stream cipher.

### Cryptanalysis	and	Brute-Force	Attack
**Cryptanalysis**: 
- Attack	relies	on	the	nature	of	the algorithm	plus	some	knowledge	of	the	 general	characteristics	of	the	plaintext.
- Attack	exploits	the	characteristics	of the	algorithm	to	attempt	to	deduce	a	
specific	plaintext	or	to	deduce	the	key being	used.

**Brute-force	attack**:
- Attacker	tries	every	possible	key	on a	piece	of	ciphertext	until	an	intelligible	translation	into	plaintext	is	obtained.
- On	average,	half	of	all	possible	keys must	be	tried	to	achieve	success.

### Types of Attacks on Encrypted Messages
**Ciphertext Only**:
- Encryption algorithm.
- Ciphertext.

**Known Plaintext**:
- Encryption algorithm.
- Ciphertext.
- One or more plaintext-ciphertext pairs formed with the secret key.
  
**Chosen Plaintext**:
- Encryption algorithm.
- Ciphertext.
- Plaintext message chosen by cryptanalyst, together with its corresponding ciphertext generated with the secret key.

**Chosen Ciphertext**:
- Encryption algorithm.
- Ciphertext.
- Plaintext message chosen by cryptanalyst, together with its corresponding ciphertext generated with the secret key.

**Chosen Text**:
- Encryption algorithm.
- Ciphertext.
- Plaintext message chosen by cryptanalyst, together with its corresponding ciphertext generated with the secret key.
- Ciphertext chosen by cryptanalyst, together with its corresponding decrypted plaintext generated with the secret key.

### Encryption Scheme Security
**Unconditionally	secure**: No	matter	how	much	time	an	opponent	has,	it	is	impossible	for	him	or	her	to	decrypt	the	 ciphertext	simply	because	the	required	information	is	not	there.

**Computationally	secure**: The	cost	of	breaking	the	cipher	exceeds	the	 value	of	the	encrypted	information. The	time	required	to	break	the	cipher exceeds	the	useful	lifetime	of	the	information

### Strong	Encryption	
The	term	*strong	encryption*	refers	to	encryption	schemes	that	make	it	impractically	difficult	for	unauthorized	persons	or	systems	to	gain	access	to	
plaintext	that	has	been	encrypted. Properties	that	make	an	encryption	algorithm	strong	are:
- Appropriate	choice	of	cryptographic	algorithm.
- Use	of	sufficiently	long	key	lengths.
- Appropriate	choice	of	protocols.
- A	well-engineered	implementation. 
- Absence	of	deliberately	introduced	hidden	flaws.

## Substitution Techniques
Substitution techniques is one	in	which	the	letters	of	plaintext	are	 replaced	by	other	letters	or	by	numbers	or symbols. If	the	plaintext	is	viewed	as	a	sequence	of	bits,	then	substitution	involves	replacing	plaintext	bit	patterns	with	ciphertext	bit	patterns. Alphabet	is	wrapped	around	so	that	the	letter	
following	Z	is	A
- `plain`:  `meet me after the toga party`
- `cipher`:	`PHHW PH	DIWHU	WKH	WRJD SDUWB`	

### Caesar Cipher	
This is the simplest	and	earliest	known	use	of	a	substitution	cipher and was used by Julius	Caesar. It involves	replacing	each	letter	of	the	alphabet	with	the	letter	standing	three	places	further	down	the	alphabet.

**Can define transformation as**:

  `a b c d e f g h i j k l m n o p q r s t u v w x y z`  
  `D E F G H I J K L M N O P Q R S T U V W X Y Z A B C`
  
**Mathematically give each letter a number**:

  `a b c d e f g h i j k l m n o p q r s t u v w x y z`  
  `0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25`
  
**Algorithm can be expressed as**:    

  `c = E(3, p) = (p + 3) mod 26`
  
**A shift may be of any amount, so that the general Caesar algorithm is**:

  `C = E(k, p) = (p + k) mod 26`
  
**Where k takes on a value in the range 1 to 25; the decryption algorithm is simply**:

  `p = D(k, C) = (C - k) mod 26`

### Monoalphabetic	Cipher
Rather	than	just	shifting	the	alphabet, this algorithm could	shuffle	the	letters	arbitrarily. Each	plaintext	letter	maps	to	a	different random	ciphertext	letter. Hence	key	is	26	letters	long.
- `Plain`: `abcdefghijklmnopqrstuvwxyz`
- `Cipher`: `DKVQFIBJWPESCXHTMYAUOLRGZN`
- `Plaintext`: `ifwewishtoreplaceletters`
- `Ciphertext`: `WIRFRWAJUHYFTSDVFSFUUFYA`	

If	the	“cipher”	line	can	be	any	permutation	of	the	 26	alphabetic	characters,	then	there	are	26!	or greater	than	4	x	1026	possible	keys. This	is	10	orders	of	magnitude	greater	than	the	key	space	for	DES. Approach	is	referred	to	as	a	*monoalphabetic	substitution*	cipher	because	a	single	cipher	alphabet	is	used	per	
message.

However, this approach is not secured due to human language are redundant. The letters are not equally commonly used. In	English,	`E`	is	by	far	the	most	common	letter, then	`T`, `R`, `N`, `I`, `O`, `A`, `S`. Other letters are fairly rare, those are `Z`, `J`, `K`, `Q`, `X`.

This algorithm is easy	to	break	because	they	reflect	the	frequency	data	of	the	original	alphabet. The countermeasure	is	to	provide	multiple	substitutes	
(homophones)	for	a	single	letter.

### Playfair Cipher
This is best know as multiple-letter	encryption	cipher and was invented	by	British	scientist	Sir	Charles	Wheatstone	in	1854. It treats	digrams	in	the	plaintext	as	single	units	and	translates	these	units	into	ciphertext	digrams. The algorithm is based	on	the	use	of	a	5	x	5	matrix	of	letters	constructed	using	a	keyword.

Fill	in	letters	of	keyword	(minus	duplicates)	from	left	to	right	and	from	top	to	bottom,	then	fill	in	the	remainder	of	the	matrix	with	the	remaining	
letters	in	alphabetic	order.

For example, the keyword is MONARCHY:

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_3/imgs/playfair_key.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Playfair key matrix - MONARCHY keyword.
</figcaption>
<br/>

In the process of encrypting and decrypting, plaintext is encrypted two letters at a time. Should a pair consist of a repeated letter, a filler, like 'X', is inserted. For instance, the word "balloon" would be encrypted as "ba lx lo on". If both letters in the pair fall within the same row, each letter is replaced with the letter to its right, wrapping back to the start if it reaches the end. As an example, “ar" would encrypt to "RM". Similarly, if both letters of the pair are in the same column, each one is replaced with the letter immediately below it, wrapping back to the top if it reaches the bottom. For example, “mu" would encrypt to "CM". In cases where the letters don't meet the aforementioned criteria, each letter is replaced by the one in its row in the column of the other letter of the pair. For instance, “hs" would encrypt as "BP", while “ea" could be encrypted to either "IM" or "JM", depending on preference.

Playfair cipher's security is improved much more over monoalphabetic since we have 26 x 26 = 676 digrams. However, it still can be broken given a few hundred letters since there still has much plaintext structure.

### Hill Cipher
The algorithm was developed	by	the	mathematician	Lester	Hill	in	1929. The strength	is	that	it	completely	hides	singleletter	frequencies. The	use	of	a	larger	matrix	hides	more	frequency	information: A	3	x	3	Hill	cipher	hides	not	only	single-letter	but	also	two-letter	frequency	information. It is strong	against	a	ciphertext-only	attack	but	easily	broken	with	a	known	plaintext	attack.

### Polyalphabetic	Ciphers	
Improves	on	the	simple	monoalphabetic	technique	by	using	different	monoalphabetic	substitutions	as one	proceeds	through	the	plaintext	message.

**Vigenère	Cipher**
- It is best	known	and	one	of	the	simplest	polyalphabetic	substitution	ciphers. In	this	scheme	the	set	of	related	monoalphabetic	substitution	rules	consists	of	the	26	Caesar ciphers	with	shifts	of	0	through	25. Each	cipher	is	denoted	by	a	key	letter	which	is	the ciphertext	letter	that	substitutes	for	the	plaintext	letter	“a”.
- To encrypt a message, a key is needed that is as long as the message. Usually, the key is a repeating keyword. For example, if the keyword is *deceptive*, the message “we are discovered save yourself” is encrypted as:
  - `key`: `deceptivedeceptivedeceptive`	
  - `plaintext`: `wearediscoveredsaveyourself`	
  - `ciphertext`:	`ZICVTWQNGRZGVTWAVZHCQYGLMGJ`
- Even	this	scheme	is	vulnerable	to	cryptanalysis because	the	key	and	the	plaintext	share	the	same frequency	distribution	of	letters,	a	statistical	
technique	can	be	applied.		

**One-Time	Pad** 
- It's an improvement to the Vernam cipher and was proposed by Army Signal Corp officer, Joseph Mauborgne.
- Key Features:
  - The key used for encryption and decryption is random and as long as the message itself. This ensures that it's not repeated.
  - After using the key for a single message, it's discarded.
  - Each new message requires a new key of the same length as that message.
- Security:
  - The scheme is deemed unbreakable.
  - The ciphertext output appears random and bears no statistical relationship to the plaintext, making it nearly impossible to infer the original message.
  - Since the ciphertext provides no information about the plaintext, there's no way to crack the code.
- Challenges:
  - Creating large quantities of truly random keys poses a practical challenge, especially for heavily used systems that might require millions of such characters.
  - The distribution of these mammoth keys is problematic because both the sender and the receiver need to possess the same key for every message.
- Utility Limitations:
  - Due to the mentioned challenges, the one-time pad is of limited utility. It's mostly used for low-bandwidth channels where very high security is paramount.
- Uniqueness: The one-time pad is the only cryptosystem that offers perfect secrecy.

## Transposition Techniques

### Rail	Fence	Cipher	
This is the simplest	transposition	cipher. Plaintext	is	written	down	as	a	sequence	of	diagonals	and	then	read	off	as	a	sequence	of	rows. To	encipher	the	message	“meet	me	after	the	toga party”	with	a	rail	fence	of	depth	2,	we	would	write:
- `m	e	m		a		t		r		h		t		g		p		r		y`
-   `e	t		e		f		e		t		e		o		a		a		t`

Thus, the encrypted message is: `MEMATRHTGPRYETEFETEOAAT`	

### Row	Transposition	Cipher	
This is	a	more	complex	transposition. We write	the	message	in	a	rectangle,	row	by	row,	and	read	the	message	off,	column	by	column,	but	permute	the	order	of	the	columns. The	order	of	the	columns	then	becomes	the	key	to	the	algorithm
- `Key`:	     `4 3 1 2 5 6 7`
- `Plaintext`: 
```sh
a t t a c k p
o s t p o n e
d u n t i l t
w o a m x y z 
```	
- `Ciphertext`:	`TTNAAPTMTSUOAODWCOIXKNLYPETZ`

## Citation
Cited as:

<blockquote>
    <summary>Classical Encryption Techniques</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_3/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023cet,
  title   = "Classical Encryption Techniques",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "September",
  url     = "https://mnguyen0226.github.io/posts/info_security_3/post/"
}
```

## References
[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Sept. 04, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_3/imgs/delaware.avif" />
</center>
<figcaption class="img_footer">
    Fig. 2: Delaware, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/a-group-of-people-walking-on-a-boardwalk-next-to-a-building-hNgFCbQZ1ZE" class="img_footer">Gary Cole @ Unsplash</a>).
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