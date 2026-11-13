# Level 16 → Level 17

Scan ports 31000-32000 to find the SSL server that returns credentials.

> 🔗 **OverTheWire page:** [Bandit Level 16 → Level 17](https://overthewire.org/wargames/bandit/bandit17.html)

## Topics Covered

- [Nmap](#now-what-is-nmap-deep-explanation) → scan ports to find open services
- [KeyUpdate message](#1-what-keyupdate-means) → and how to avoid it with `-nocommands`

## Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don't. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

## Commands You May Need

- [ssh](https://manpages.ubuntu.com/manpages/noble/man1/ssh.1.html)
- `telnet`
- `nc`
- `ncat`
- `socat`
- `openssl`
- `s_client`
- `nmap`
- `netstat`
- `ss`

## Important Notes

> **Helpful note: Getting "DONE", "RENEGOTIATING" or "KEYUPDATE"? Read the "CONNECTED COMMANDS" section in the manpage.**

## Helpful Reading Material

- [Port scanner on Wikipedia](https://en.wikipedia.org/wiki/Port_scanner)

## Solution

### Step 1

**What the Bandit question is asking**

The challenge says:

**Find which port between 31000 and 32000 has a server listening on it.**

This means:

- There are many "doors" (ports).
- Only some doors have a program behind them.
- You must check every door from **31000 → 32000**.
- The correct one will respond and will later be used with SSL.

The easiest way to do this is with **Nmap**. Run this command:

```bash
nmap -p31000-32000 localhost
```

Look at the screenshot.

![Terminal showing the nmap scan of ports 31000 to 32000 on localhost with five open ports](../assets/bandit/level16/01-nmap-open-ports.png)

### Step 2

As you see from the Nmap result, there are 5 ports open on the server. Let's check which one is the port that provides the secure session, so it's the right port to send and receive the data we targeted. Let's go through them one by one.

![Terminal showing openssl s_client failing on port 31046 because it does not speak SSL](../assets/bandit/level16/02-openssl-port-31046-error.png)

### Step 3

I have already tried them one by one. The only port that seems to have the secure connection is 31790. However, when we tried to connect to it, send the password and wait for the credentials, it gives us a KEYUPDATE message!

![Terminal showing the KEYUPDATE message returned after sending the password](../assets/bandit/level16/03-keyupdate-message.png)

To know more about the KeyUpdate message and how to overcome all possible errors, see the bit of theory below.

### Step 4

For this challenge, we overcome it by typing `-nocommands` as an option at the end of the command to avoid the misinterpretation, and it will accept the password normally and send us back the credentials.

```bash
openssl s_client -connect localhost:31790 -nocommands
```

![Terminal showing openssl s_client with the -nocommands option connecting to port 31790](../assets/bandit/level16/04-openssl-nocommands.png)

## A Bit of Theory

### Now, what is Nmap? (Deep explanation)

Nmap = **N**etwork **Map**per  
It is one of the most powerful tools in cybersecurity.

### ✔ 1. Nmap scans ports

Nmap can check whether ports are:

- **open** → a program is listening

- **closed** → nothing is listening

- **filtered** → blocked by firewall

This is exactly what you’re doing in Bandit.

### ✔ 2. Nmap discovers services

Nmap can tell you:

- what application is running

- whether it uses SSL

- what version it is

- what protocol it uses

Example output:

80/tcp open http

443/tcp open https

22/tcp open ssh

Very useful in ethical hacking.

### ✔ 3. Nmap can detect operating systems

Using special packet signatures, Nmap can guess:

- Linux

- Windows

- even the exact distribution

(Not needed in Bandit, but important to know.)

### ✔ 4. Nmap can scan networks, not just localhost

You can use Nmap to scan:

- other devices

- subnets

- entire networks

Example:

```bash
nmap 192.168.1.0/24
```

It will list all active devices.

### ✔ 5. Nmap uses different scanning techniques

Nmap has multiple scan types:

- SYN scan (stealth scan) → default

- Connect scan

- UDP scan

- Version detection scan

- Firewall evasion

You're using a basic TCP scan, which is enough for Bandit.

- ✔ You found 5 open ports — good

- ✔ Now scan only those for SSL

- ✔ Look for the one port that shows SSL/TLS

- ✔ Connect using:

```bash
openssl s_client -connect localhost:<ssl_port>
```

- ✔ Paste password → get next password

### 1. What “KeyUpdate” Means

**KeyUpdate** is a **TLS 1.3 feature**.  
It allows either side of a TLS connection (client or server) to **refresh encryption keys during a live session**, *without renegotiating a whole handshake*.

This improves forward secrecy by periodically rotating keys used to encrypt traffic.

From the OpenSSL documentation and StackOverflow explanation I found:

- A TLS 1.3 KeyUpdate “updates the sending cryptographic keys and optionally asks the peer to update theirs.” [\[docs.openssl.org\]](https://docs.openssl.org/3.2/man3/SSL_key_update/)

- OpenSSL’s s_client triggers a KeyUpdate when the input line **begins with K or k**, but **ONLY if TLS 1.3 is in use**. [\[stackoverflow.com\]](https://stackoverflow.com/questions/58547963/openssl-keyupdate-and-ssl-key-updatewrong-ssl-version)

### 2. Why Does Typing a Password Trigger KeyUpdate?

This is the part that confuses a lot of Bandit players like me.

In openssl s_client **interactive mode**, once the TLS connection is established, certain **single-character commands** control the client. They are *not sent to the server*.

OpenSSL defines k and K as:

- **k / K → Send a TLS 1.3 KeyUpdate message**  
  (instead of sending the text you typed) [\[stackoverflow.com\]](https://stackoverflow.com/questions/58547963/openssl-keyupdate-and-ssl-key-updatewrong-ssl-version)

This means:

- ✔ Even if you type a whole password (e.g. kSkvUpMQ7l...),

**OpenSSL looks ONLY at the first character.**

If that first character is:

- k → KeyUpdate

- R → renegotiation

- Q → quit

- …and so on.

This behavior is confirmed in analysis of a real case where the string kSkvUp... triggered KEYUPDATE:

“My arbitrary string was conflicting with the KEYUPDATE Connected Command.” [\[icecandidate.com\]](https://icecandidate.com/posts/openssl_conflicting_commands/)

So your password *is* being typed correctly, the **first character** is simply being misinterpreted as an OpenSSL command.

We can stop such feature by using -quiet or -nocommands

### ✅ 3. What -quiet Does

-quiet:

- ✔ Disables interactive command letters (like k, R, Q)

- ✔ Suppresses session/certificate output

- ✔ Turns on -ign_eof and -nocommands implicitly

Meaning:

- Your input is treated as **raw data**

- No connected commands are processed

- Your password is sent *exactly* as typed

OpenSSL documentation:

“-quiet inhibits printing session info… implicitly turns on -ign_eof and -nocommands.” [\[docs.openssl.org\]](https://docs.openssl.org/master/man1/openssl-s_client/)

This is why Bandit guides tell you to use:

```bash
openssl s_client -connect localhost:31790 -quiet
```

So that your password beginning with k won't trigger KeyUpdate. [\[nerdiverset.no\]](https://nerdiverset.no/over-the-wire/bandit/bandit-level-16/)

### ✅ 4. What -nocommands Does

-nocommands:

- ✔ Directly disables ALL interactive one-letter commands

This includes k, K, R, Q, etc.

Once -nocommands is set:

- The client will **no longer interpret the first character of your input**

- Everything you type is sent directly to the server

From the explanation of preventing conflicting commands:

“The -nocommands parameter disables interactive command letters. This allows strings to be passed without conflicting.” [\[icecandidate.com\]](https://icecandidate.com/posts/openssl_conflicting_commands/)

Useful alternative to -quiet when you still want normal output.
