# Introduction to Cryptography

## History

First signs of cryptography are in 1466 in a writing about cyphers of L.B.Alberti. Alan Turing in 1936 published a paper about the Enigma machine. In 1945 the first public key cryptography was published by Whitfield Diffie and Martin Hellman. In 1976 the first public key cryptography was published by Whitfield Diffie and Martin Hellman.

## Cryptography

Cryptography is the science and study of secret writing (**security mechanism**). It is a branch of Cryptology, which contains cryptoanalysis.

It contains mechanism to:

- scrable data

- make data available only to authorized users

So cryptography role is to keep data secret and veriify its integrity.

## Cryptosystems

A cryptosystem is a set of rules that define how to encrypt and decrypt data. It is composed of:

1. Encryption algorithm **E**

2. Decryption algorithm **D**

3. Plaintext **M**

4. Keys **K**

5. Cipher text **C**
- E: M \* K -> C

- D: C \* K -> M

> An application of cryptography is communication security. It is used to protect data in transit. It is used also in secure computing, to protect data at rest (multi-machine).

**The Kerckhoffs’ principle** affirm that the key should be the only secret in a cryptosystem: you shouldn't trust the secrecy of the algorithm.

## Keys

A key is an input to a cryptographic algorithm used to obtain confidentiality, integrity, authenticity or other property over some data.

A _keyspace_ is the set of all possible keys. A _key length_ is the number of bits in a key. _Entropy_ is the variance in keys.

Keys should be as random as possible and secured safely. The security of a key depends on the distribution method between parties.

## Computational Security

You talk about computational security when you talk about the time needed to break a cryptosystem. If time is longer than the importance of the data, the cryptosystem is secure. This is considering a **brute force attack**.

A **trapdoor one-way function** is a function that is easy to compute in one direction, but hard to compute in the other direction unless you have some additional information.

A _hash_ is a one-way function, an _encryption_ is a trapdoor one-way function.

While hash functions are used for integrity, encryption is used for confidentiality.

## Encryption

There are two types of transformations:

- substitution: where each element on the plain text is mapped to another element

- transposition: elements are rearranged

No information should be lost.

### Substitution Cyphers

A substitution cypher is a method of encrypting where each unit of data is replaced with cipher text, accroding to a fixed system.

#### Caesar Cipher

In the caesar chipher each letter was substituted with another letter, which is a fixed number of positions down the alphabet. The key is the number of positions.

![](/home/samu/Documents/Markdown/images/ComputerAndNetworkSecurity/caesarCipher.png)

**Mathematically**: $e(x) = (x + k) \mod 26$, $d(x) = (x - k) \mod 26$

This method is easy to break through brute force or thinking about the frequency of letters in the language to allign the letters.

#### Vigeneré Cipher

In the vigeneré cipher a keyword is chosen, then the position of the plaintext's letter is summed with the position of the keyword's letter and you follow the caesar method. A key of size _l_ make up the keyspace ($l^{26}$) and it becomes more complex as you increase the lenght of the key.

![](/home/samu/Documents/Markdown/images/ComputerAndNetworkSecurity/vigenereCipher.png)

A -> 0, L->11 = first letter L (11)

- T -> 19, E->4 = second letter X (23)

- T-> 19, M->12 = third letter F (5)

- ...

### Transposition Ciphers

In a transposition cipher the plaintext is rearranged in a different order. The key is the **permutation** of symbols.

#### Columnar Cipher

In the columnar cipher the plaintext is written in a grid, of a fixed number of columns. The ciphertext is then read by columns.

![](/home/samu/Documents/Markdown/images/ComputerAndNetworkSecurity/columnarCipher.png)

### Modern Crypto

Because of the quick development of the computer, it become easier to decrypt the ciphertext.

New encryption technique, based on algoritms and bits, were introduced:

- stream encryption

- block encryption

- public-key encyption

#### Symmetric Key Cryptography

In symmetric key cryptography a single key of encryption and decryption is used. All the parties involved in the communication must share the same key. A symmetric key crypto is usually very fast (like a XOR operation for stream ciphers, or for block ciphers).

#### Stream Ciphers

In a stream cipher the plaintext is encrypted one bit at a time. The key is a stream of bits, which is XORed with the plaintext.

> Example: GSM traffic encryption A5/1, E0 in bluetooth, RC4 (SSL)

#### Block Ciphers

In a block cipher the plaintext is divided in blocks, and each block is encrypted with the same key. The key is a stream of bits, which is XORed with the plaintext.

> Example: Data Encryption Standard (DES), Advanced Encryption Standard (AES)

##### DES

DES is a block cipher with a 64-bit block size and a 56-bit key. It is a Feistel cipher, which is a symmetric key block cipher. Half of the block is used as input to a function, which is then XORed with the other half of the block. The output of the function is then XORed with the other half of the block. The process is repeated for the other half of the block. In each round, the key is permuted from the original.

DES was cracked in 1997 by a group of researchers at the University of California, Berkeley, with a computer that parallelized the brute force attack.

##### AES

The encryption process is based on a series of table lookups and XOR operations. The key is expanded as the rounds performed.

#### Asymmetric Key Cryptography

Also called Public Key Cryptography: it allows two parties to engage in a secure communication without sharing a secret key. The key is composed of a public key and a private key. The public key is used to encrypt the message, and the private key is used to decrypt the message.

PKC is based on one-way functions (multiplication/factorization, exponentiation/logarithm).

It is used foor two purposes:

- keep the plaintext secret and only visible to the recipient (**data confidentiality**)

- be sure that the sender is the one who sent the message (**signature**)

![](/home/samu/Documents/Markdown/images/ComputerAndNetworkSecurity/examplePKC.png)

##### RSA - Rivest-Shamir-Adleman

RSA is an asymmetric key algorithm based on the factoring problem. It is based on the fact that it is easy to multiply two large numbers, but it is hard to factorize them.

A recent problem of RSA encryption is the generation of keys: the attacker could compute the private part of an RSA key, particularly if the key is a common 1024 or 2048 bits.

RSA can be use for integrity: from the message a hash is generated and encrypted with the private key; the signature is sent with the message. The receiver can decrypt the hash and compare it with the hash of the message.

##### DH - Diffie-Hellman

This is based on the fact that its easy to compute exponents, but hard to compute discrete logarithms.

![DH algorithm representation](https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Diffie-Hellman_Key_Exchange.svg/250px-Diffie-Hellman_Key_Exchange.svg.png)

Security of DH depends on the difficulty of the Discrete Logarithm Problem. DH is a key agreement protocol, which means that it is used to agree on a shared secret key and it does not provide authentication.

# Applications of Cryptography

## Remarks on PKC

**pros**:

- private key is never transmitted

- confidentiality

- non-repudiation

**cons**:

- slow

- how to distribute the public key?

- problems of identity in authentication

To mitigate the cons, **Digital Signatures** are used.

> For example it is important to protect OTA updates, because if the update is not signed, the attacker could modify the update and install a malicious version.

## Public Key Infrastructure

To work the main requirement of the Public Key Infrastructure is that the public key must be associated with the identity of the user who is controlling the private key. A second requirement is that parties can assure that binding is still valid.

The initial proposal were bulletin boards where puclic keys were listed. However this required trust in the provider of the bulletin board. Another solution (implemented for IoT) is to hardcore the public key in the software.

> CVE-321: use of hardcoded keys

The most adopted solution are **digital certificates**.

### Digital Certificates

A digital certificate is a file that contains the public key of a user, and is signed by a trusted authority (called **Trusted Third Party** or **Certificate Authority**). The certificate is used to authenticate the user.

The certificate contains:

- Issuer: the name of the CA

- Subject: the name of the user

- Subject Public Key Info: the public key of the user

- Issuer Digital Signature: the signature of the CA

> The sandard for digital certificates is X.509

PKI is composed of:

- **Certificate Authority**: the trusted third party that issues the certificates

- **Registration Authority**: assure valid and correct registration of the user

- **Validation Authority**: provides an entity information

- **Distribution System**

- repository of certificates LDAP

- Certificate Revocation List (CRL)

**How to obtain a certificate**

1. the user generates a key pair

2. user sends a certificate request to the CA

3. CA responds with his public key digitally signed (so it can be verified the integrity)

4. user gather all information

5. user send a certificate request to the CA with his public key signed (**Client Signing Request**)

6. CA gets the public key from the user and verifies the signature

7. CA issues the certificate

## SSL/TLS

Secure Sockets Layer (SSL) is a protocol for secure communication over the Internet. It is based on PKC and digital certificates. Transport Layer Security (TLS) is the successor of SSL.

SSL/TLS is used to guarantee:

- communicaton with the exact website the user intended to connect to

- content is not modified during transmission

### TLS in Client-Server Communication

TLS consist of two protocols:

- **Handshake Protocol**: used to establish a secure connection

- **Record Protocol**: used to encrypt the data

PKC is used in the handshake phase to negotiate the cipher suite, authenticate and establish keys used in the record protocol. Symmetric key cryptography is used in the record protocol to encrypt the data.

Additionally TLS provide a Change Cipher Protocol and an Alert Protocol.

### TLS Handshake Protocol

1. Client sends a Client Hello message to the server (version, cipher suites)

_cipher suites are set of algorithms that help secure a network connection that uses TLS. It is composed by a key exchange algorithm, a bulk encryption algorithm and a message authentication code_

> TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256:
> 
> - key exchange: ECDHE (Ephimeral Diffie Hellman), auth during handshake
> 
> - bulk encryption: AES_128_GCM, encrypt message stream
> 
> - message authentication: SHA256, authenticate message stream

2. Server sends a Server Hello message to the client (version, cipher suite, session ID)

3. Server sends a Certificate message to the client (certificate of the server); it also sets the premaster secret and might request a client certificate

4. If the client is required to send a certificate, it sends a Certificate message to the server; it also sets the premaster secret, and verifies the server certificate

5. Each of the two parties sends a Change Cipher Spec message (single byte = 1) and a finished message (hash of the handshake messages)

6. From now on, the communication is encrypted using the shared key

_more on_ [Cloudflare about TLS](https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/)

### TLS for Authentication

- **server**: client encrypt data with public key of the server, so only the server can decrypt it

- **client**: server decrypt data with public key of the client, so it knows that the client is the one who sent the data

### TLS for Confidentiality

All messages are encrypted with the algorithm and the key negotiated during the handshake.

### TLS for Integrity

Given by the MAC (Message Authentication Code) negotiated during the handshake. MAC are similar to hash functions, but they use the same key both for encryption and decryption.

### TLS Vulnerablilities

There are a few vulnerabilities in TLS:

- Backward compatibility

- Logical flaws

- Implementation issues

**Nonces**: a nonce is a random number that is used only once. It is used to prevent replay attacks. It is the base of the challenge-response authentication.

> The server sends a nonce to the client, the client encrypts it with the private key and sends it back to the server. The server decrypts it with the public key and checks if the nonce is the same.

**Vulnerabilities Examples**:

- RC4NOMORE: based of decryption of cookies

- POODLE: MiM makes the client use a less secure cipher suite (SSLv3)

- BLEICHENBACHER: MiM can recover the premaster secret

- HEARTBLEED: MiM can recover the memory of the server sending a crafted packet

MORAL: deprecate RSA for key exchange

### Notes on TLS 1.3

- Remove unsafe features

- More encryption

- Increased performance (hello + key exchange in one message, use of pre-shared keys)

- Backwards compatibility
