---
author: "Minh T. Nguyen"
title: "Information and Network Security Concepts"
date: "2023-08-21"
description: "An exploration of computer security, delving into the OSI security architecture, various security attacks, and models for network protection. This guide also covers essential security services, mechanisms, potential attack surfaces, and principles"
tags: ["cybersecurity", "long-read"]
categories: ["information security"]
series: ["Information Security"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>[v.1.0] (08/21/2023):</strong> Post started!</p>

The field of cybersecurity consists of: measures of deter, prevent, detect, and correct security violations that involve the storage, processing, and transmission of information.

## Computer Security Objectives: CIA
**Confidentiality**:
- Data confidentiality: assures that private or confidential information is not made available or disclosed to unauthorized individuals.
- Privacy: assures that individuals control or influence what information related to them may be collected and stored and by whom and to whom that information may be disclosed.
- Ex: Student grad information is an assert whose confidentiality is considered to be highly important by students.

**Integrity**:
- Data integrity: assures that information and programs are changed only in a specified and authorized manner.
- System integrity: assures that a system performs its intended function in an unpaired manner, free from deliberate or inadvertent unauthorized manipulation of the system.
- Ex: Patient information stored in the database - inaccurate info could result in serious harm or death to a patient and expose the hospital to massive liability.

**Availability**: assures that the systems work promptly and service is not denied to authorized users.
- Ex: An online telephone directory lookup application would be classified as a low-availability requirement.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_1/imgs/cia_triad_1.png" />
</center>
<figcaption class="img_footer">
    Fig. 1: CIA Triad.
</figcaption>
<br/>

*Privacy is not security, but security is necessary to achieve privacy (it is not sufficient).*

**Authencity:** verifying that users are who they say they are and that each input arriving at the system cam from a trusted source.

**Accountability:** the security goal that generates that requirement for actions of an entity to be traced uniquely to that entity.

## The OSI Security Architecture
**Security attack:** any action that compromised the security of information owned by an organization.

**Security mechanism:** a process (or a device incorporating such a process) that is designed to detect, prevent, or recover from a security attack.

**Security service:** a process or communication service that enhances the security of the data processing systems and the information transfers of an organization. Intended to counter security attacks and they make use of one or more security mechanism to provide the service.

## Security Attacks
**Threat:** a potential for violation of security, which exists when there is a circumstance, capability, action, or event that could breach security and cause harm. That is, a threat is a possible danger that might exploit a vulnerability.

**Attack:** an assault on system security that derives from an intelligent threat; that is, an intelligent act that is deliberate attempt (especially in the sense of a method or technique) to evade security services and violate the security policy of a system.

**Passive attack:** attempts to learn or make use of info from the system but does not affect system resources, such as monitoring and eavesdrop. There are 2 types:
- The release of message contents.
- Traffic analysis

**Active attack:** attempts to alter system resources or affect their operation, such as modify, abuse resources. There are 4 types:
- Masquerade: Takes place when one entity pretends to be a different entity. Usually includes one of the other forms of active attack.
- Replay: Involves the passive capture of a data unit and its subsequent retransmission to produce an unauthorized effect.
- Modification of messages: Some portion of a legitimate message is altered, or messages are delayed or reordered to produce an unauthorized effect. 
- Denial of service: Prevents or inhibits the normal use or management of communications facilities.

## Security Services
**Authentication**: concerned with assuring that a communication is authentic.

**Access control**: is the ability to limit and control the access to the host system and the applicaiton via communication links. To achieve this, each entity trying to gain access must first be identified, or authenticated, so that access rights can be tailored to the individual.

**Data Confidentiality**: is both the protection of transmitted data from passive attacks or the protection of traffic flow from analysis.

**Data Integrity**: is a connectionless integrity service deals with individual messages without regard to any larger context or generally provides protection against message modification only. *I don't care if you know the info but I do care if you modify it*.

**Nonrepudiation**: prevents either sender or receiver from denying a transmitted message. When a message is sent, the receiver can prove that the alleged sender in fact send the message. When a message is received, the sender can prove that the alleged receiver in fact received the message.

**Avalability of services**: addresses the security concerns raised by denial-of-service attacks.

## Security Mechanisms
**Cryptographic algorithms**: we can distinguish between reversible cryptographic mechanisms and irreversible cryptographic mechanisms.

**Data integrity**: covers a variety of mechanisms used to assure the integrity of a data unit or stream of data units.

**Digital signature**: data appended to, or a cryptographic transformation of, a data unit that allows a recipient of the data unit to prove the source and integrity of data unit and protect against forgery.

**Authentication exchange**: a mechanism intended to ensure the identity of an entity by means of information exchange.

**Access control**: a variety of mechanisms that enforce access rights to resources.

**Traffic padding**: the insertion of bits into gaps in a data stream to frustrate traffic analysis attempts.

**Routing control**: enables selections of particular physically or logically ensure routes for certain data.

**Notarization**: the use of a trusted third party to assure certain properties of a data exchange.

## Cryptography
Crytographic algorithms and protocols can be grouped into 4 main areas:
- **Symmetric encryption**: used to conceal the contents of blokcs or streams of data of any size, including messages, files, encryption keys, and passwords.
- **Asymmetric encryption**: used to conceal small blocks of data, such as encryptionn keys and hash function values, which are used in digital signatures.
- **Data integrity algorithms**: used to protect blocks of data, such as messages, from alteration.
- **Authentication protocols**: schemes based on the used of cryptographic algorithms designed to authenticate the identity of entities.

<center>
    <img style="width: 80%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_1/imgs/crypto_types.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Types of cryptographic algorithms.
</figcaption>
<br/>

**Keyless algorithms**: a pseudorandom number generator produces a deterministic sequence of numbers or bits that has the appearance of being a truly random sequence.

**Single-key algorithms:** depends on the use of a secret key.

**Asymmetric (two keys) algorithms**: a pair of keys are used instead of only one shared secret key.

## Fundametals of Security Design Principles
**Economy of mechanism**: the design of security measures embodied in both hardware and software should be as simple and small as possible.

**Fail-safe default**: access decisions should be based on permission rather than exclusion - the default situation is lack of access, and the protection scheme identifies conditions under which access is permitted.

**Complete mediation**: every access much be checked against the access control mechanism.

**Open design**: the design of a security mechanism should be open rather than secret.

**Separation of priviledge**: a practice in which multiple privilege attributes are required to achieve access to restricted resource.

**Least privilege**: every process and every user of the system should operate using the least set of privileges necessary to perform the task.

**Least common mechanism**: the design should minimize the functions shared by different users, providing mutual security.

**Psychological acceptability**: security mechanisms should not interfere unduly with the work of users, while at the same time metting the needs of those who authorize access.

**Isolation**: a principle that applies in 3 contexts
- Public access systems should be isolated from critical resources to prevent disclosure to tampering.
- The processes and files of individual users should be isolated from one another except where it is explicitly desired.
- Security mechanisms should be isolated in the sense of preventing access to those mechanisms.

**Encapsulation**: viewed as a specific form of isolation based on object-oriented functionality.

**Modularity**: refers both to the development of security functions as separate, protected modules and to the use of modular architecture for mechanism design and implementation.

**Layering**: referes to the use of multiple, overlapping protection approaches addressing the people, technology, and operational aspects of the information systems.

**Least astonishment**: a program or user interface should always respond in the way that least likely to astonish the user.

## Attack surface
**Network attack surface**: vulnerabilities over an enterprise network, wide-area network, or internet.

**Software attack surface**: vulnerabilities in application, utility, or OS code.

**Human attack surface**: vulnerabilities created by personnel or outsiders such as social engineering, human error, and trusted insiders.

<center>
    <img style="width: 80%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/info_security_1/imgs/ad_surface.png" />
</center>
<figcaption class="img_footer">
    Fig. 3: Defense in depth and attack surface.
</figcaption>
<br/>


## Citation
Cited as:

<blockquote>
    <summary>Information and Network Security Concepts</summary>
    <summary>https://mnguyen0226.github.io/posts/info_security/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mtl,
  title   = "Information and Network Security Concepts",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "August",
  url     = "https://mnguyen0226.github.io/posts/info_security_1/post/"
}
```

## References
[1] Pearson, https://www.pearson.com/en-us/subject-catalog/p/Stallings-Pearson-e-Text-for-Cryptography-and-Network-Security-Principles-and-Practice-Access-Card-8th-Edition/P200000003477 (accessed Aug. 21, 2023). 


<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/scale_from_zero_to_millions_of_users/imgs/golden_bridge.png" />
</center>
<figcaption class="img_footer">
    Fig. 2: Golden Gate Bridge, San Francisco, U.S.A </br>(Image Source: 
    <a href="https://unsplash.com/photos/gZXx8lKAb7Y" class="img_footer">Maarten van den Heuvel @ Unsplash</a>).
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