# Bandit Writeups
<p align="center">
  <img alt="Wargames" src="https://img.shields.io/badge/OverTheWire-Wargames-blue">
  <img alt="Bandit" src="https://img.shields.io/badge/Bandit-completed-brightgreen">
  <img alt="Topic" src="https://img.shields.io/badge/topic-cybersecurity-red">
  <img alt="Purpose" src="https://img.shields.io/badge/purpose-educational-red">
<img alt="focus" src="https://img.shields.io/badge/focus-Linux-red">
</p>

> 🔗 **Official game page:** [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) · [Start at Level 0](https://overthewire.org/wargames/bandit/bandit0.html)

This folder has my **solutions, write-ups and walkthroughs** for the Bandit wargame from OverTheWire. Bandit is made for beginners, and it is a great way to master Linux, because every level teaches you a new command line skill by making you use it.

I wrote these as I learned, in my own words. Each level is explained **step by step**, with **screenshots** from my terminal, and a **theory** section that explains the idea behind the solution, so you don't only get the answer, you understand why it works.

## Start Here

- [Bandit overview](overview.md): what OverTheWire is and how it works
- [Level 0](level0.md): how to connect to the server with SSH

## How Each Walkthrough Is Organized

1. 🔗 A link to the **official OverTheWire level page**
2. **Topics Covered**: a quick reference to the new topics of the level, linked to their explanation
3. **Level Goal** and **Commands You May Need**
4. **Solution**: numbered steps, with the screenshot right after the step it shows
5. **A Bit of Theory**: the concepts behind the solution

## What You Will Practice

- Navigating the file system, reading files and finding things (`ls`, `cat`, `find`, `grep`)
- Working with text: pipes, redirection, `sort`, `uniq`, `strings`, `diff`
- Encoding and compression: base64, ROT13, hexdump, `gzip`, `bzip2`, `tar`
- SSH, private keys, ports, `nc`, `openssl` and `nmap`
- File permissions and setuid binaries
- Cron jobs and writing shell scripts
- Escaping restricted shells
- Git: clone, history, branches, tags and push

## All Levels

### Levels 0 → 10: Linux command line basics

| Level | Walkthrough & main topic | OverTheWire |
|-------|----------------------------|-------------|
| 0 → 1 | [Reading a file with `ls` and `cat`](level0-to-level1.md) | [Level page](https://overthewire.org/wargames/bandit/bandit1.html) |
| 1 → 2 | [Files named with a dash](level1-to-level2.md) | [Level page](https://overthewire.org/wargames/bandit/bandit2.html) |
| 2 → 3 | [Spaces in file names](level2-to-level3.md) | [Level page](https://overthewire.org/wargames/bandit/bandit3.html) |
| 3 → 4 | [Hidden files](level3-to-level4.md) | [Level page](https://overthewire.org/wargames/bandit/bandit4.html) |
| 4 → 5 | [Finding the human-readable file with `file`](level4-to-level5.md) | [Level page](https://overthewire.org/wargames/bandit/bandit5.html) |
| 5 → 6 | [Searching with `find`](level5-to-level6-add-permession-level.md) | [Level page](https://overthewire.org/wargames/bandit/bandit6.html) |
| 6 → 7 | [Searching the whole system and redirecting errors](level6-to-level7.md) | [Level page](https://overthewire.org/wargames/bandit/bandit7.html) |
| 7 → 8 | [Searching inside files with `grep`](level7-to-level8.md) | [Level page](https://overthewire.org/wargames/bandit/bandit8.html) |
| 8 → 9 | [Unique lines with `sort`, `uniq` and pipes](level8-to-level9.md) | [Level page](https://overthewire.org/wargames/bandit/bandit9.html) |
| 9 → 10 | [Readable text in binary files with `strings`](level9-to-level10.md) | [Level page](https://overthewire.org/wargames/bandit/bandit10.html) |

### Levels 10 → 20: Encoding, compression, SSH keys and networking

| Level | Walkthrough & main topic | OverTheWire |
|-------|----------------------------|-------------|
| 10 → 11 | [Base64 decoding](level10-to-level11.md) | [Level page](https://overthewire.org/wargames/bandit/bandit11.html) |
| 11 → 12 | [ROT13 and the Caesar cipher with `tr`](level11-to-level12.md) | [Level page](https://overthewire.org/wargames/bandit/bandit12.html) |
| 12 → 13 | [Hexdump and repeated compression](level12-to-level13.md) | [Level page](https://overthewire.org/wargames/bandit/bandit13.html) |
| 13 → 14 | [Logging in with a private SSH key](level13-to-level14.md) | [Level page](https://overthewire.org/wargames/bandit/bandit14.html) |
| 14 → 15 | [Sending data to a port with `nc`](level14-to-level15.md) | [Level page](https://overthewire.org/wargames/bandit/bandit15.html) |
| 15 → 16 | [Encrypted connections with SSL/TLS](level15-to-level16.md) | [Level page](https://overthewire.org/wargames/bandit/bandit16.html) |
| 16 → 17 | [Port scanning with `nmap`](level16-to-level17.md) | [Level page](https://overthewire.org/wargames/bandit/bandit17.html) |
| 17 → 18 | [Comparing files with `diff`](level17-to-level18.md) | [Level page](https://overthewire.org/wargames/bandit/bandit18.html) |
| 18 → 19 | [Running a command through `ssh`](level18-to-level19.md) | [Level page](https://overthewire.org/wargames/bandit/bandit19.html) |
| 19 → 20 | [setuid binaries](level19-to-level20.md) | [Level page](https://overthewire.org/wargames/bandit/bandit20.html) |

### Levels 20 → 25: Netcat, cron jobs and scripting

| Level | Walkthrough & main topic | OverTheWire |
|-------|----------------------------|-------------|
| 20 → 21 | [Netcat listener and a setuid client](level20-to-level21.md) | [Level page](https://overthewire.org/wargames/bandit/bandit21.html) |
| 21 → 22 | [Cron jobs](level21-to-level22.md) | [Level page](https://overthewire.org/wargames/bandit/bandit22.html) |
| 22 → 23 | [Reading a cron script and MD5 hashing](level22-to-level23.md) | [Level page](https://overthewire.org/wargames/bandit/bandit23.html) |
| 23 → 24 | [Writing your own shell script for cron](level23-to-level24.md) | [Level page](https://overthewire.org/wargames/bandit/bandit24.html) |
| 24 → 25 | [Brute forcing a pincode with Python sockets](level24-to-level25.md) | [Level page](https://overthewire.org/wargames/bandit/bandit25.html) |

### Levels 25 → 34: Restricted shells and git

| Level | Walkthrough & main topic | OverTheWire |
|-------|----------------------------|-------------|
| 25 → 26 | [Escaping a restricted shell with `more` and `vim`](level25-to-level26.md) | [Level page](https://overthewire.org/wargames/bandit/bandit26.html) |
| 26 → 27 | [Getting a real shell from vim](level26-to-level27.md) | [Level page](https://overthewire.org/wargames/bandit/bandit27.html) |
| 27 → 28 | [Cloning a git repository](level27-to-level28.md) | [Level page](https://overthewire.org/wargames/bandit/bandit28.html) |
| 28 → 29 | [Finding secrets in git history](level28-to-level29.md) | [Level page](https://overthewire.org/wargames/bandit/bandit29.html) |
| 29 → 30 | [Git branches](level29-to-level30.md) | [Level page](https://overthewire.org/wargames/bandit/bandit30.html) |
| 30 → 31 | [Git tags](level30-to-level31.md) | [Level page](https://overthewire.org/wargames/bandit/bandit31.html) |
| 31 → 32 | [Pushing to a repository and `.gitignore`](level31-to-level32.md) | [Level page](https://overthewire.org/wargames/bandit/bandit32.html) |
| 32 → 33 | [Escaping the uppercase shell with `$0`](level32-to-level33.md) | [Level page](https://overthewire.org/wargames/bandit/bandit33.html) |
| 33 → 34 | [The end of Bandit](level33-to-level34.md) | [Level page](https://overthewire.org/wargames/bandit/bandit34.html) |

## Back to the Main Page

- [Repository README](../README.md)
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/)

> For educational purposes only. Try each level yourself first, and use these write-ups to understand the ideas, not to copy answers.
