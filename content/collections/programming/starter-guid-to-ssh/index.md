---
title: Starter guid to SSH (Secure Shell)
published: true
date: 2021-06-14
author: Hatim
Tags: ["progamming"]
description: Welcome to our comprehensive tutorial to SSH (Secure Shell) key configuration.  This lesson will show you how to create SSH keys from scratch, as well as how to manage numerous keys and key pairs.
keywords: ssh,secure,sheel,guid,user,client,connect,host,ecryption,decryption,commands
image: /images/images-markus.png
---

# Starter guid to SSH

## What is SSH?

SSH or Secure Shell allows people to access your server remotely. It uses encryption technology to ensure that all communications to and from the server are encrypted.

It provides you with a way to authenticate remote users, pass input from the client to the host, and pass information to the client.

Linux and macOS users can use the terminal to connect directly to their remote server via SSH. Windows users should use tools like Putty.

You can use shell commands like you actually use a remote computer.

## Starting a SSH session.

The SSH command is divided into three parts:

```bash
ssh {user}@{host}
```

SSH tells the system that you want to open an encrypted connection. The user is the account you want to access (for example, root === admin). The host is the computer (IP address or domain) you want to access. After entering these, you will be prompted to enter your password. Although nothing is displayed on the screen, your password is being sent.

## SSH encryption technology.

- **Symmetric Encryption**

* **Asymmetric Encryption**

* **Hash**

### Symmetric encryption

This type of encryption uses a key for both parties to encrypt and decrypt the message.

It is usually called shared key or shared secret encryption.

Usually, there is only one key, but you can also have a key pair, one of which can calculate the other.

Both the client and the server use the agreed method (key exchange algorithm) to obtain the key, and the key will never be shown to any third party.

Information shared between the server and the client can be intercepted by another machine, but the key exchange algorithm cannot be calculated.

There are many passwords to create the key, but before secure transmission, choose one based on the order of preference of the two machines.

### Asymmetric encryption

Here we use two different keys for encryption and decryption.

This is like a one-way relationship. The public key is public, but you cannot find the private key based on the public key. The relationship between the two is complicated.

This one-way relationship means that the public key cannot decrypt its own messages, nor can it decrypt any information sent by the private key.

It is not used to encrypt the entire session, but only during the key exchange algorithm.

Before a secure connection, both machines will create temporary public-private keys and share them to create a shared key.

Once the secure symmetric communication is done, the server will use the client's public key to challenge it and send it to the client for authentication.

If the client can decrypt the message, it means they have the private key. Then you can start an SSH session.

### Hash

A communication method that will never be cracked. The hash generates a unique fixed-length value for each character in the communication that is transmitted.

This makes reverse engineering nearly impossible (until quantum computing emerges..)

It is easy to generate a hash from the input, so if the client has the correct input, it can compare it with the hash and confirm that it has the correct input.

SSH uses hashes to verify the validity of messages.

HMAC : Hash-based message authentication code is used to ensure that the message has not been intercepted or modified.

When choosing an asymmetric encryption algorithm, you must also design a message authentication algorithm, just like the password selection above.

### Mac

Each message must contain a MAC. This is calculated using the symmetric key, packet sequence number, and message content.

SSH works on TCP port 22 by default. The server listens for incoming connections on port 22.

Authenticate the secure connection and start the shell environment.

The client machine must initiate the connection by initiating the TCP handshake with the server to confirm the secure symmetric connection.

You must verify that the server ID matches the above record normally stored in the RDA Keystore file.

The connection has two stages, first both machines must agree on the encryption standards and then the user has to be authenticated with their password etc.

## Common SSH command

**1. Access a remoter server**

```bash
ssh username@hostname_or_ip
```

**2. Use a Different Port Number for SSH Connection**

```bash
ssh test.server.com -p 3322
```

**3. Generate SSH Keys Using SSH Keygen**

```bash
ssh-keygen -t rsa
```

**4. Copy file remotely usig SCP**

```bash
scp file user@remotehost:/home/username/dest
```

**5. Restart SSH service**

```bash
sudo ssh service restart
```
