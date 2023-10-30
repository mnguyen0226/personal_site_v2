---
author: "Minh T. Nguyen"
title: "Public-Key Cryptography and RSA"
date: "2023-10-18"
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

<p style="color: #286EE0"><strong>[v.1.0] (10/18/2023):</strong> Post started!</p>

## Principles of Public-Key Cryptosystems
### Public-Key Cryptosystems
About:
- Radically different approach [Diffie-Hellman76, RSA78].
- Sender, receiver do not share secret key.
- Public encryption key known to all.
- Private decryption key known only to receiver.

A	public-key	encryption	scheme	has	six	ingredients:	
- **Plaintext**: The readable message or data that is input into the encryption algorithm.
- **Encryption Algorithm**: Performs various transformations on the plaintext to produce ciphertext.
- **Public Key**: Used specifically for the encryption process. This key can be shared openly.
- **Private Key**: Used for either encryption or decryption. This key remains confidential.
- **Ciphertext**: The scrambled version of the original message, produced as output from the encryption process.
- **Decryption Algorithm**: Takes in the ciphertext and the appropriate key (either public or private) to reproduce the original plaintext.

### Terminology Related to Asymmetric Encryption
- A**symmetric Keys**: Two related keys, a public key and a private key that are used to perform complementary operations, such as encryption and decryption or signature generation and signature verification.
- **Public Key Certificate**: A digital document issued and digitally signed by the private key of a Certification Authority that binds the name of a subscriber to a public key. The certificate indicates that the subscriber identified in the certificate has sole control and access to the corresponding private key.
- **Public Key (Asymmetric) Cryptographic Algorithm**: A cryptographic algorithm that uses two related keys, a public key and a private key. The two keys have the property that deriving the private key from the public key is computationally infeasible.
- **Public Key Infrastructure (PKI)**: A set of policies, processes, server platforms, software and workstations used for the purpose of administering certificates and public-private key pairs, including the ability to issue, maintain, and revoke public key certificates.

### Misconceptions	Concerning	Public-Key	Encryption	
- Public-key	encryption	is	more	secure	from	cryptanalysis	than	symmetric	encryption.	
- Public-key	encryption	is	a	general-purpose	technique	that	has	made	symmetric encryption	obsolete.
- There	is	a	feeling	that	key	distribution	is	trivial	when	using	public-key	encryption,	compared	to	the	cumbersome	handshaking	involved	with	key	distribution	centers	for	symmetric	encryption.

### Principles	of	Public-Key	Cryptosystems
The	concept	of	public-key	cryptography	evolved	from	an	attempt	to	attack	two	of	the	most	difficult	problems	associated	with	symmetric	encryption:	
- Key	distribution: How	to	have	secure	communications	in	general	without	having	to	
trust	a	KDC	with	your	key.
- Digital	signatures: How	to	verify	that	a	message	comes	intact	from	the	claimed	sender

Whitfield	Diffie	and	Martin	Hellman	from	Stanford	University	achieved	a	breakthrough	in	1976	by	coming	up	with	a	method	that	addressed	key	distribution	problem	and	was	radically	different	from	all	previous	approaches	to	cryptography.

### Conventional vs Public-Key Encryption
**Conventional Encryption**
- Needed to Work:
  - The same algorithm with the same key is used for encryption and decryption.
  - The sender and receiver must share the algorithm and the key.

- Needed for Security:
  - The key must be kept secret.
  - It must be impossible or at least impractical to decipher a message if the key is kept secret.
  - Knowledge of the algorithm plus samples of ciphertext must be insufficient to determine the key.

**Public-Key Encryption**
- Needed to Work:
  - One algorithm is used for encryption and a related algorithm for decryption with a pair of keys, one for encryption and one for decryption.
  - The sender and receiver must each have one of the matched pair of keys (not the same one).
- Needed for Security:
  - One of the two keys must be kept secret.
  - It must be impossible or at least impractical to decipher a message if one of the keys is kept secret.
  - Knowledge of the algorithm plus one of the keys plus samples of ciphertext must be insufficient to determine the other key.

### Applications for Public-Key Cryptosystems 
Public-key	cryptosystems	can	be	classified	into	three	categories:
- Encryption/decryption: The	sender	encrypts	a	message	with	the	recipient’s	public	key.
- Digital signature: the	sender	“signs”	a	message	 Digital	signature	 with	its	private	key.
- Key exchange: Two sides cooperate to exchange a session key.

Some	algorithms	are	suitable	for	all	three	applications,	whereas	others	can	be	used	only	for	one	or	two.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_9/imgs/pkc.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Applications for Public-Key Cryptosystems.
</figcaption>
<br/>

### Requirements for Public-Key Cryptography 
**Conditions	that	these	algorithms	must	fulfill**:	
- It	is	computationally	easy	for	a	party	B	to	generate	a	pair	(publickey	PUb, private	key	PRb).	
- It	is	computationally	easy	for	a	sender	A,	knowing	the	public	key	and	the	message	to	be	encrypted,	to	generate	the	corresponding	ciphertext.		
- It	is	computationally	easy	for	the	receiver	B	to	decrypt	the	resulting	ciphertext	using	the	private	key	to	recover	the	original	message.	
- It	is	computationally	infeasible	for	an	adversary,	knowing	the	public	key,	to	determine	the	private	key.	
- It	is	computationally	infeasible	for	an	adversary,	knowing	the	public	key	and	a	ciphertext,	to	recover	the	original	message.	
- The	two	keys	can	be	applied	in	either	order.


**Need a trap-door one-way function**
- A one-way function is one that maps a domain into a range such that every function value has a unique inverse, with the condition that the calculation of the function is easy, whereas the calculation of the inverse is infeasible
  - Y = f(X) easy
  - X = f^(-1)(Y) infeasible

**A trap-door one-way function is a family of invertible functions f_k**, such that:
- Y = f_k(X) easy, if k and X are known
- X = f_k^(-1)(Y) easy, if k and Y are known
- X = f_k^(-1)(Y) infeasible, if Y known but k not known

**A practical public-key scheme depends on a suitable trap-door one-way function**

### Public-Key Cryptanalysis 
A	public-key	encryption	scheme	is	vulnerable	to	a	brute-force	attack	
- Countermeasure:		use	large	keys.	
- Key	size	must	be	small	enough	for	practical	encryption	and	decryption.	
- Key	sizes	that	have	been	proposed	result	in	encryption/decryption	speeds	that	are	too	slow	for	general-purpose	use.	
- Public-key	encryption	is	currently	confined	to	key	management	and	signature	applications.	

Another	form	of	attack	is	to	find	some	way	to	compute	the	private	key	given	the	public	key. To	date	it	has	not	been	mathematically	proven	that	this	form	of	attack	is	infeasible	for	a	particular	public-key	algorithm.	

Finally,	there	is	a	probable-message	attack	This	attack	can	be	thwarted	by	appending	some	random	bits	to	bits	to	the	messages.

## The RSA Algorithm
### Rivest-Shamir-Adleman	(RSA)	Algorithm
Developed	in	1977	at	MIT	by	Ron	Rivest,	Adi	Shamir	&	Len	Adleman. Most	widely	used	general-purpose	approach	to	public-key	encryption.	Is	a	cipher	in	which	the	plaintext	and	ciphertext are	integers	between	`0`	and	`n	–	1`	for	some	`n`. A	typical	size	for	n	is	1024	bits,	or	309	decimal	digits	

RSA	makes	use	of	an	expression	with	exponentials. Plaintext	is	encrypted	in	blocks	with	each	block	having	a	binary	value	less	than	some	number	n.	Encryption	and	decryption	are	of	the	following	form,	for	some	plaintext	block	M	and	ciphertext block	`C`:	
- `C	=	M^e mod	n`	
- `M	=	C^d	mod	n	=	(M^e)^d	mod	n	=	M^(ed)	mod	n`		

Both	sender	and	receiver	must	know	the	value	of	`n`. The	sender	knows	the	value	of	`e`,	and	only	the	receiver	knows	the	value	of	`d`. This	is	a	public-key	encryption	algorithm	with	a	public	key	of	`PU={e,n}`	and	a	private	key	of	`PR={d,n}`.		

### RSA:	Creating	public/private	key	pair
1.	choose	two	large	prime	numbers	p,	q.			
2.	compute	n	=	pq,		z	=	(p-1)(q-1)	
3.	choose	e	(with	e < n)	that	has	no	common	factors		with	z	(e,	z are	“relatively	prime”).	
4.	choose	d	such	that	ed-1	is		exactly	divisible	by	z. (in	other	words:	ed	mod	z		=	1	).	
5. public	key	is	(n,e).		private	key	is	(n,d).	

### RSA:	encryption,	decryption
0. given	(n,e)	and	(n,d)	as	computed	above	
1. to	encrypt	message	m	(< n),	compute	c	=	m^e mod n	
2. to	decrypt	received	bit	pattern,	c,	compute	m	=	c^d	mod	n	
3. m =	(m^e mod n)^d	 mod n

### Why	is	RSA	secure?
Suppose	you	know	Bob’s	public	key	(n,e).	How	hard	is	it	to	determine	d? Essentially	need	to	find	factors	of	n	without	knowing	the	two	factors	p	and	q.
- Fact:	factoring	a	big	number	is	hard.

### Algorithm	Requirements
For	this	algorithm	to	be	satisfactory	for	publickey	encryption,	the	following requirements	must	be	met:	
1. It	is	possible	to	find	values	of	e,	d,	n	such	that	Med	mod	n	=	M	for	all	M	<	n.
2. It	is	relatively	easy	to	calculate	Me 	mod	n	and	Cd	mod	n	for	all	values	of	M	<	n.
3. It	is	infeasible	to	determine	d	given	e	and	n.

### Exponentiation	in	Modular	Arithmetic
- Both	encryption	and	decryption	in	RSA	involve	raising	an	integer	to	an	integer	power,	mod	n. 
- Can	make	use	of	a	property	of	modular	arithmetic:	[(a	mod	n)	x	(b	mod	n)]	mod	n	=(a	x	b)	mod	n.
- With	RSA	you	are	dealing	with	potentially	large	exponents	so	efficiency	of exponentiation	is	a	consideration.

### Efficient	Operation	Using	the	Public	Key
To	speed	up	the	operation	of	the	RSA	algorithm	using	the	public	key,	a	specific	choice	of	e	is	usually	made.

The	most	common	choice	is	65537	(2^16	+	1)	
- Two	other	popular	choices	are	e=3	and	e=17.	
- Each	of	these	choices	has	only	two	1	bits,	so	the	number	of	multiplications	required	to	perform	exponentiation	is	minimized.	
- With	a	very	small	public	key,	such	as	e	=	3,	RSA	becomes	vulnerable	to	a	simple	attack.

### Efficient	Operation	Using	the	Private	Key
- Decryption	uses	exponentiation	to	power	d.	
- A	small	value	of	d	is	vulnerable	to	a	brute-force	attack	and	to	other	forms	of	cryptanalysis.	
- Can	use	the	Chinese	Remainder	Theorem	(CRT)	to	speed	up	computation.	
  - The	quantities	d	mod	(p	–	1)	and	d	mod	(q	–	1)	can	be	precalculated.	
  - End	result	is	that	the	calculation	is	approximately	four	times	as	fast	as	evaluating	M	=	Cd mod	n	directly.	

### Key	Generation
Before	the	application	of	the	public-key	cryptosystem	each	participant	must	generate	a	pair	of	keys:	
- Determine	two	prime	numbers	p	and	q.		
- Select	either	e	or	d	and	calculate	the	other.

Because	the	value	of	n	=	pq will	be	known	to	any	potential	adversary,	primes must	be	chosen	from	a	sufficiently	large	set. The	method	used	for	finding	large	primes	must	be	reasonably	efficient.

### Procedure	for	Picking	a	Prime	Number
1. Pick	an	odd	integer	n	at	random	
2. Pick	an	integer	a	<	n	at	random	
3. Perform	the	probabilistic	primality	test	with	a	as	a	parameter.		If	n	fails	the	test,	reject	the	value	n	and	go	to	step	1	
4. If	n	has	passed	a	sufficient	number	of	tests,	accept	n;	otherwise,	go	to	step	2

### Breaking	an	encryption	scheme
- Cipher-text	only	attack:	Trudy	has	ciphertext	she	can	analyze.	
- Two	approaches:	brute	force:	search	through	all	keys; statistical	analysis.	
- Known-plaintext	attack:	Trudy	has	plaintext	corresponding	to	ciphertext.	
  - e.g.,	in	monoalphabetic	cipher,	Trudy	determines	pairings	for	a,l,i,c,e,b,o,	
- Chosen-plaintext	attack:	Trudy	can	get	ciphertext	for	chosen	plaintext.

## The Security of RSA 

**Five possible approaches to attacking RSA are:**

1. **Chosen ciphertext attacks**
   - This type of attack exploits properties of the RSA algorithm.

2. **Brute force**
   - Involves trying all possible private keys.

3. **Mathematical attacks**
   - There are several approaches, all equivalent in effort to factoring the product of two primes.

4. **Hardware fault-based attack**
   - This involves inducing hardware faults in the processor that is generating digital signatures.

5. **Timing attacks**
   - These depend on the running time of the decryption algorithm.

### Factoring	Problem	
We	can	identify	three	approaches	to	attacking	RSA	mathematically:	
- Factor	n	into	its	two	prime	factors.	This	enables	calculation	of	ø(n)	=	(p	–	1)	x	(q	–	1),	which	in	turn	enables	determination	of	d	=	e-1	(mod	ø(n))	
- Determine	ø(n)	directly	without	first	determining	p	and	q.	Again,	this	enables	determination	of	d	=	e-1 (mod	ø(n))
- Determine	d	directly	without	first	determining	ø(n)

### Timing	Attacks
Paul	Kocher,	a	cryptographic	consultant,	demonstrated	that	a	snooper	can	determine	a	private	key	by	keeping	track	of	how	long	a	computer	takes	to	decipher	messages	

Are	applicable	not	just	to	RSA	but	to	other	publickey	cryptography	systems	

Are	alarming	for	two	reasons: It	comes	from	a	completely	unexpected	direction. It	is	a	ciphertext-only	attack

### Countermeasures	
- Constant exponentiation time: Ensure that all exponentiations take the same amount of time before returning a result; this is a simple fix but does degrade performance.
- Random delay: Better performance could be achieved by adding a random delay to the exponentiation algorithm to confuse the timing attack.
- Blinding: Multiply the ciphertext by a random number before performing exponentiation; this process prevents the attacker from knowing what ciphertext bits are being processed inside the computer and therefore prevents the bit-by-bit analysis essential to the timing attack.


### Fault-Based	Attack	
An	attack	on	a	processor	that	is	generating	RSA	digital	signatures. Induces	faults	in	the	signature	computation	by	reducing	the	power	to	the	processor. The	faults	cause	the	software	to	produce	invalid	signatures	which	can	then	be	analyzed	by	the	attacker	to	recover	the	private	key.

The	attack	algorithm	involves	inducing	single-bit	errors	and	observing	the	results.	

While	worthy	of	consideration,	this	attack	does	not	appear	to	be	a	serious	threat	to	RSA. It	requires	that	the	attacker	have	physical	access	to	the	target	machine	and	is	able	to	directly	control	the	input	power	to	the	processor.

### Chosen	Ciphertext	Attack	(CCA)
The	adversary	chooses	a	number	of	ciphertexts	and	is	then	given	the	corresponding	plaintexts,	decrypted	with	the	target’s	private	key. Thus	the	adversary	could	select	a	plaintext,	encrypt	it	with	the	target’s	public	key,	and	then	be	able	to	get	the	plaintext	back	by	having	it	decrypted	with	the	private	key.	The	adversary	exploits	properties	of	RSA	and	selects	blocks	of	data	that,	when	processed	using	the	target’s	private	key,	yield	information	needed	for	cryptanalysis.

To	counter	such	attacks,	RSA	Security	Inc.	recommends	modifying	the	plaintext	using	a	procedure	known	as	optimal	asymmetric	encryption	padding	(OAEP).	

## Citation
Cited as:

<blockquote>
    <summary>Public-Key Cryptography and RSA</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_2/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "Public-Key Cryptography and RSA",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "October",
  url     = "https://mnguyen0226.github.io/posts/info_security_9/post/"
}
```

## References

[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Oct. 18, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_9/imgs/indiana.avif" />
</center>
<figcaption class="img_footer">
    Fig. 2: Indiana, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/green-grass-field-during-sunset-lN9uP-G3x-Q" class="img_footer">Hannah Hutson @ Unsplash</a>).
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