# Level 0

Learn how to connect to the Bandit server using SSH.

> 🔗 **OverTheWire page:** [Bandit Level 0](https://overthewire.org/wargames/bandit/bandit0.html)

## Topics Covered

- [SSH](#what-is-ssh) → how we connect to the Bandit server
- [Port 2220](#so-why-does-overthewire-use-port-2220-instead-of-22) → why Bandit does not use the normal SSH port
- [Command line vs GUI](#should-i-use-the-command-line-only-cant-i-interact-with-overthewire-through-a-gui) → why we work in the terminal

## Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **bandit0**. Once logged in, go to the [Level 1](https://overthewire.org/wargames/bandit/bandit1.html) page to find out how to beat Level 1.

## Commands You May Need

- [ssh](https://manpages.ubuntu.com/manpages/noble/man1/ssh.1.html)

## Helpful Reading Material

- [Secure Shell (SSH) on Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell)
- [How to use SSH with a non-standard port on It's FOSS](https://itsfoss.com/ssh-to-port/)
- [How to use SSH with ssh-keys on wikiHow](https://www.wikihow.com/Use-SSH)

## Important Notes

> Since you connect via SSH, every command you type in your terminal will be executed on the remote Linux server.
>
> You can't run Windows commands there, as you access a Linux machine.

## Solution

### Step 1

Learn how to connect via SSH. Each level is a remote Linux machine you log into. You should use the credentials in the top corner and log in using the SSH protocol.

If this is the first time you hear about the SSH protocol, see the [theory below](#a-bit-of-theory).

### Step 2

For example, to start Bandit, in your terminal:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

- `bandit0` → username
- `bandit.labs.overthewire.org` → hostname
- `-p 2220` → the port number

### Step 3

As you can see, you are logging in to the `bandit.labs.overthewire.org` host on port 2220, where the Bandit wargame is located. You are logged in as a `bandit0` user, having only `bandit0` privileges. For instance, there are some limitations in reading, writing, and creating files or directories. Each level has its own permissions.

### Step 4

Then it will welcome you and ask for the password. The password for `bandit0` is `bandit0`, while you should find the password for each upcoming level by solving the challenge.

## A Bit of Theory

### What is SSH?

Imagine that you are an administrator and you want to do your usual administration tasks on a remote device located in a different city. Should you always visit it on site to change a password or update packages? The SSH protocol is the solution.

**S**ecure **Sh**ell protocol is a secure protocol used to connect to a remote machine via the command line.

You typically use it as follows, in your terminal:

```bash
ssh username@hostname
```

`ssh` uses port 22 as the default port number. If you wish to use a different port, use `-p` followed by the target port.

**Think of it like this:**

A secure tunnel between your device and the target machine. Everything being sent through this tunnel is encrypted. No one can understand your interaction unless they have the right key.

Once you are connected using the right credentials, you can access the machine under the user privileges you log in as, as if you were sitting in front of it.

### So Why Does OverTheWire Use Port 2220 Instead of 22?

OTW uses port 2220 for multiple reasons:

1. **To avoid conflict with normal SSH traffic**

   Port 22 is usually used for administrative access and internal maintenance. Using the same port for thousands of learners could cause collisions or security issues.

2. **To separate and isolate each wargame environment**

   Ports act like **doors**. Each game has its own "door", leading to its own isolated environment.

3. **To teach cybersecurity enthusiasts that real servers often use custom ports**

   Custom ports reduce brute-force attempts, hide the service from internet bots, and allow running multiple SSH services in parallel.

### Should I Use the Command Line Only? Can't I Interact with OverTheWire Through a GUI?

Absolutely, you should interact with the OverTheWire server through the command line. OTW challenges aim to teach you cybersecurity concepts where command line skills are essential. Also, remote servers rarely rely on a GUI as it is heavy and consumes resources.

In early computers, the sole way to interact with the OS was through the command line. Later, the graphical user interface allowed users to do almost everything with fancy graphics. However, the CLI is still the most reliable and fastest way to finish your tasks on a computer.

Take this for example: imagine that you want to check your IP address. How many clicks does it take to find it?

What if you decided to do it via the CLI? You would open your terminal and type `ipconfig`, and all your essential network information would appear without further ado. You see, instead of making ten clicks and moving your mouse to every corner of the screen, you can do whatever you want without even raising your hand from the keyboard. How efficient!
