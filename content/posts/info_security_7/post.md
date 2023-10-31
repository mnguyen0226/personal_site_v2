---
author: "Minh T. Nguyen"
title: "Block Cipher Operation"
date: "2023-10-02"
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

<p style="color: #286EE0"><strong>[v.1.0] (10/02/2023):</strong> Post started!</p>

## Multiple Encryption and Triple DES
### Meet-in-the-Middle	Attack	
The	use	of	double	Data Encryption Standard (DES) results	in	a	mapping	that	is	not	equivalent	to	a	single	DES	encryption.

The	meet-in-the-middle	attack	algorithm	will	attack	this	scheme	and	does	not	depend	on	any	particular	property	of	DES	but	will	work	against	any block	encryption	cipher.

### Triple	DES	with	Three	Keys	
Many	researchers	now	feel	that	three-key	3DES	is	the	preferred	alternative. A	number	of	Internet-based	applications	have	adopted	three-key	3DES	including	PGP	and	S/MIME.

## Electronic Codebook
### Modes	of	Operation
A	technique	for	enhancing	the	effect	of	a	cryptographic	algorithm	or	adapting	the	algorithm	for	an	application.

To	apply	a	block	cipher	in	a	variety	of	applications,	five	modes	of	operation	have	been	defined	by	NIST.
- The	five	modes	are	intended	to	cover	a	wide	variety	of	applications	of	encryption	for	which	a	block	cipher	could	be	used.
- These	modes	are	intended	for	use	with	any	symmetric	block	cipher,	including	triple	DES	and	AES.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_7/imgs/bcm.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: Block Cipher Modes of Operation.
</figcaption>
<br/>

### Advantages	and	Limitations	of	ECB	
Repetitions	in	message	may	show	in	ciphertext:
- if	aligned	with	message	block.		
- particularly	with	data	such	graphics/images.		
- or	with	messages	that	change	very	little,	which	become	a	code-book	analysis	problem.		

Weakness	due	to	encrypted	message	blocks	being	independent.		

Main	use	is	sending	a	few	blocks	of	data.	

Criteria	and	properties	for	evaluating	and	constructing	block	cipher	modes	of	operation	that	are	superior	to	ECB:	
- Overhead.
- Error	recovery.
- Error	propagation.
- Diffusion.
- Security.

### Advantages	and	Limitations	of	CBC	
Each	ciphertext	block	depends	on	all	previous	message	blocks. Thus	a	change	in	the	message	block	affects	all	the	following	ciphertext	blocks	as	well	as	the	original	block. Need	Initial	Value	(IV)	known	to	sender	&	receiver. Either	IV	must	be	a	fixed	value	or	it	must	be	sent	encrypted	in	ECB	mode	before	rest	of	message. At	end	of	message,	handle	possible	last	short	block by	padding	with	known	non-data	value	(e.g.,	nulls).

### Advantages of	CTR
- Hardware	efficiency.	
- Software	efficiency.	
- Preprocessing.	
- Random	access.	
- Provable	security.	
- Simplicity.	

## XTS-AES Mode for Block-Oriented Storage Devices
Approved	as	an	additional	block	cipher	mode	of	operation	by	NIST	in	2010.

Mode	is	also	an	IEEE	Standard,	IEEE	Std 1619-2007.
- Standard	describes	a	method	of	encryption	for	data	stored	in	sector-based	devices	where	the	threat	model	includes	possible	access	to	stored	data	by	the	adversary.	
- Has	received	widespread	industry	support.

### Tweakable	Block	Ciphers	
XTS-AES	mode	is	based	on	the	concept	of	a	tweakable	block	cipher.

Tweak	need	not	be	kept	secret: purpose	is	to	provide	variability

### Storage	Encryption	Requirements
The	requirements	for	encrypting	stored	data,	also	referred	to	as	“data	
at	rest”,	differ	somewhat	from	those	for	transmitted	data.

The	P1619	standard	was	designed	to	have	the	following	characteristics:	
- The	ciphertext	is	freely	available	for	an	attacker.
- The	data	layout	is	not	changed	on	the	storage	medium	and	in	transit.	
- Data	are	accessed	in	fixed	sized	blocks,	independently	from	each	other.	
- Encryption	is	performed	in	16-byte	blocks,	independently	from	each	other.	
- There	are	no	other	metadata	used,	except	the	location	of	the	data	blocks
within	the	whole	data	set.	
- The	same	plaintext	is	encrypted	to	different	ciphertexts	at	different	
locations,	but	always	to	the	same	ciphertext	when	written	to	the	same	
location	again.	
- A	standard	conformant	device	can	be	constructed	for	decryption	of	data	
encrypted	by	another	standard	conformant	device.	

## Citation
Cited as:

<blockquote>
    <summary>Block Cipher Operation</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security_7/post/</summary>
</blockquote>

Or 

```sh
@article{nguyen2023bco,
  title   = "Block Cipher Operation",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "October",
  url     = "https://mnguyen0226.github.io/posts/info_security_7/post/"
}
```

## References
[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Oct. 02, 2023). 

<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_7/imgs/boise.avif" />
</center>
<figcaption class="img_footer">
    Fig. 2: Boise, Idaho, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/gray-blue-and-black-concrete-city-buildings-cBx1EygM3BM" class="img_footer">Alden Skeie @ Unsplash</a>).
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