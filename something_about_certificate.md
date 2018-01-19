<!-- TOC -->

- [Something About Public Key Certificate](#something-about-public-key-certificate)
    - [Public Key Certificate](#public-key-certificate)
        - [What is public key certificate?](#what-is-public-key-certificate)
        - [Why we use certificate?](#why-we-use-certificate)
        - [How does certificate work](#how-does-certificate-work)
    - [Usage](#usage)
    - [How to generate root certificate?](#how-to-generate-root-certificate)
    - [How to sign server certificate?](#how-to-sign-server-certificate)
    - [How to sign client certificate?](#how-to-sign-client-certificate)

<!-- /TOC -->


# Something About Public Key Certificate

## Public Key Certificate

### What is public key certificate?

Before introducing certificate, I would like to start with RSA that is a famous cryptosystem using public key to encrypt data and using private key which is secret to decrypt encrypted data.
Up to now, the RSA algorithm remains unhackable due to the limitations of calculating ability.
In cryptography, a public key certificate, also known as a digital certificate or identity certificate, is an electronic document used to prove the ownership of a public key.

### Why we use certificate?

By using the certificate, people do not have to worry about that some bad guy change the original public key that you want to use it for encrypting data to his own public key so that he can use his private key to decrypt your data.
This is really useful especially in communication though the network. Because on the network, client and server cannot preset the keys for encrypting. So client and server have to talk about the keys before they start exchanging some secrets. Since they do not have keys for encrypted now, their talks about the keys can be insecure if someone wants to start a Man-in-the-middle attack. At this moment, it is very smart to use the certificate to protect the server's public key.

### How does certificate work

First, there must be some third-party organization that both client and server trust and we call them **certificate authority** (CA).
Then the server that wants to use HTTPS to protect their communication with client should generate a pair of keys containing private key and public key.
After this, the server should generate the **certificate request** file usually follow by `.csr` which contains the server's public key.
Then the CAs use their own secret key to encrypt the `.csr` file, which is usually we called **signature**.
Signature will generate a `.crt` file that is usually called certificate and will be send back to the server later.
After all these things done, now the server has a pair of keys whose public key is encrypted in the `.crt` file by the CAs' private key.
Now, let's see what will happen if a client wants to connect to the server though HTTPS. 
First of all, the client send an unencrypted message to the server to ask for connection.
Then, the server return a piece of raw message, a piece of encrypted message, by its private key, and the certificate.
Next, when the client receive these messages, they first decrypted the certificate to get the server's public key.
By the way, because the certificate was encrypted by the CAs's private key and everyone trust the CAs, the client should save the public keys of the CAs before to establish a secure connection.
Then the client use the public key to decrypt the secure message sent by the server in order to compare it with the raw messages.
Once the match, the client knows that this server is the real server which I want to talk with.
At last, the client and the server randomly generate a key which is used for **symmetric-key algorithm** for the next encryption of the real messages.
Well, now the certificate successfully protect the public key of the server and ensure the client to connect to the real server to keep people from Man-in-the-middle attack.

## Usage

## How to generate root certificate?

## How to sign server certificate?

## How to sign client certificate?