# Level 19 → Level 20

Use the provided setuid binary to access `/etc/bandit_pass`.

> 🔗 **OverTheWire page:** [Bandit Level 19 → Level 20](https://overthewire.org/wargames/bandit/bandit20.html)

## Topics Covered

- [setuid and setgid](#what-do-setuid-and-setgid-actually-mean-and-how-to-set-them) → run a program as its owner

## Level Goal

To gain access to the next level, you should use the setuid binary in the home directory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Helpful Reading Material

- [setuid on Wikipedia](https://en.wikipedia.org/wiki/Setuid)

## Important Notes

> Concept: setuid

## Solution

### Step 1

When we tried `ls -la`, we got into this file `bandit20-do` with the permissions `rwsr-xr-x`.

![Terminal showing ls -la with the setuid binary bandit20-do and the unreadable output of cat on it](../assets/bandit/level19/01-bandit20-do-setuid-binary.png)

The `s` in the user permissions means setuid, and it means to run this executable file under the owner's permissions. This file is a binary file that allows us to execute commands with elevated privileges.

### Step 2

We will benefit from that by using `cat` on the file that contains the password of bandit20.

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

![Terminal showing bandit20-do run with whoami and then used to cat the password file](../assets/bandit/level19/02-bandit20-do-reading-password.png)

## A Bit of Theory

### What do setuid and setgid actually mean and how to set them?

### Set setuid (user ID bit)

This makes the program run as **the file’s owner**.

```bash
chmod u+s filename
```

Permissions will show:

`-rwsr-xr-x`

The **s** in the user field means setuid is ON.

### Set setgid (group ID bit)

This makes the program run as **the file’s group**.

```bash
chmod g+s filename
```

Permissions will show:

`-rwxr-sr-x`

The **s** in the group field means setgid is ON.

### ✅ 2. How to use (benefit from) setuid/setgid

In Bandit, **you DO NOT have permission** to set setuid or setgid yourself.  
Instead, the challenge gives you **an already setuid/setgid binary**, and you must use it.

### ✅ How you benefit from them

When you run a file that has:

**setuid → you temporarily “become” the file owner**

**setgid → you temporarily “become” the file’s group**

Bandit uses this so that:

- A binary owned by **bandit20**

- With setgid or setuid enabled

- Allows YOU (bandit19) to run it as **bandit20**

- And therefore read the next password!

### 3. How it applies to Bandit Level 19

In Bandit Level 19:

- You find a binary with permissions similar to:

-rwsr-x--- 1 bandit20 bandit19 something

This means:

**When you run that binary, it runs as bandit20**  
It can read /etc/bandit_pass/bandit20  
That’s how you get the password for the next level

Just run it like any other program:

```bash
./filename
./bandit20-do cat /etc/bandit_pass/bandit20
```

The binary bandit20-do runs as **bandit20**, so the command inside runs with bandit20’s privileges.
