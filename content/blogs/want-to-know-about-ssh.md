+++
date = '2019-07-24T22:16:36+05:30'
draft = false
title = 'Secure Shell (SSH)'
+++
![](/images/hugo-ssh.png)

For a beginner, who just started playing with computers, SSH (Secure Shell) is basically a set of rules which provides a secure connection between two computers. It can be used to securely connect a computer to a remote computer. For example Developers or System Admins could continue their work while they're on vacation on another country using SSH.
The way SSH works is by making use of a client-server model to allow for authentication of two remote machines and encryption of the data that passes between them.
There are three different types of encryptions used by SSH.

1. Symmetric encryption
2. Asymmetric encryption
3. Hashing

These techniques are used to maintain data transmission in ciphertext (written in a secret code). In the world of cryptography, specific ciphers are usually cracked at some point, and new stronger ciphers are developed. So SSH implementations will drop older ciphers and support newer ciphers over time.

### Symmetric Encryption:

In symmetric encryption, only one key (let's say private key or secret key) is used both for encryption and decryption of the data transferred between client and server. Anyone who holds the 'one key' can decrypt the data.
The process of creating a symmetric key is carried out by a key exchange algorithm.

Key Exchange Algorithm is a method of securely exchanging cryptographic keys between two parties. If the sender and receiver wish to exchange encrypted messages then each must be encrypt the messages to be sent and decrypt the messages received.

### Asymmetric Encryption:

In asymmetric encryption, both keys (private as well as public key) are used for encryption and decryption.
Suppose Tux wants to send some data to Nux. So Tux uses Nux's public key to encrypt data for it. Nux, on the other hand, uses its private key to decrypt the data which was encrypted by its public key. Similarly, if Nux wants to send some data to Tux then Tux's public key is used by Nux to encrypt the data and Tux's private key is used to decrypt the data.

So which one is used in SSH?
SSH uses both symmetric and asymmetric encryption. Since asymmetric encryption is more time consuming, most of the SSH connections use symmetric encryption.

Want to know how SSH works? Check it out:
[How Secure Shell Works (SSH)](https://www.youtube.com/watch?v=ORcvSkgdA58)


