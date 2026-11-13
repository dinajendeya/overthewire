# Level 13 → Level 14

Use the SSH private key provided to log into the next level.

> 🔗 **OverTheWire page:** [Bandit Level 13 → Level 14](https://overthewire.org/wargames/bandit/bandit14.html)

## Topics Covered

- [Private SSH key](#1-what-does-it-mean-if-you-have-a-private-ssh-key) → log in without typing a password
- [chmod](#chmod) → change file permissions

## Level Goal

The password for the next level is stored in **/etc/bandit_pass/bandit14 and can only be read by user bandit14**. For this level, you don't get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous Bandit levels, and find out how to use the key for this level.

If you need help with this level: a hint file can be found in the home directory.

Make sure to read the error messages as they are informative.

## Commands You May Need

- [ssh](https://manpages.ubuntu.com/manpages/noble/man1/ssh.1.html)
- `scp`
- `umask`
- `chmod`
- [cat](https://manpages.ubuntu.com/manpages/noble/man1/cat.1.html)
- `nc`
- `install`

## Helpful Reading Material

- [SSH/OpenSSH/Keys](https://help.ubuntu.com/community/SSH/OpenSSH/Keys)
- [Transferring Files via SCP](https://help.ubuntu.com/community/SSH/TransferFiles)

## Solution

### Step 1

After finding the human-readable file from the last level, we found out that this is a private key. Actually, it is the one that we should use to log in to this level instead of our usual way.

So I hope you copied the text that came from the last challenge and saved it. Remember, we didn't find any password, so let's see how we can use the private key to log in.

![Terminal showing the home directory with the sshkey.private file and the content of the HINT file](../assets/bandit/level13/01-home-directory-and-hint-file.png)

### Step 2

At first, we copied the private key and saved it on our machine. Our own machine, not the OverTheWire server. If you are on Windows, use `Notepad++` **not** `Notepad` so it keeps the text formatting correct and never damages the text.

![The private key opened in the nano editor and saved as bandit.key](../assets/bandit/level13/02-private-key-in-nano.png)

### Step 3

Now we tried using the normal way but failed to log in. We added the `-i` option so we can attach the private key file while connecting to the server.

```bash
ssh -i bandit14.key bandit14@bandit.labs.overthewire.org -p 2220
```

![Terminal showing ssh with the -i option failing because the private key permissions are too open](../assets/bandit/level13/03-ssh-key-permissions-too-open.png)

Still it doesn't work, and the reason is clear from the login banner. It says the permissions for the private key file are too open, as it appears in the image, so we need to change them using the `chmod` command and then try again.

### Step 4

```bash
chmod 600 bandit14.key
ssh -i bandit14.key bandit14@bandit.labs.overthewire.org -p 2220
```

Let's dive deep into the private key and the `chmod` command.

## A Bit of Theory

### 1. What Does It Mean if You Have a Private SSH Key?

A **private SSH key** is a *secret cryptographic key* that proves **your identity** when connecting to a remote machine over SSH.

It's like a **password**, but much stronger, something that should **never be shared**. A key only works if the server has the matching **public key**.

If you have a private key file (example: id_rsa or keyfile), it means: **You are authorized to access a specific SSH account on a remote server**  
(assuming you also know the correct username).

An example format: ***RSA PRIVATE KEY* (PEM) format.**

That means your key **should look like this**:

```text
-----BEGIN RSA PRIVATE KEY-----
MIIE...
...lots of base64 lines...
...2E2aEzA==
-----END RSA PRIVATE KEY-----
```

### 2. How You Benefit From a Private SSH Key

You shouldn't share your private key with anyone or paste it onto the internet

With a private key, you can:

- **Log in without a password**

- Access restricted systems where only key-based login is allowed

- Authenticate securely during CTF, penetration‑testing labs, and OTW challenges

### 3. How to Use a Private SSH Key to Log In

To use a private key, you run:

```bash
ssh -i <private_key_file> <username>@<host>
```

For example:

```bash
ssh -i bandit.key bandit14@bandit.labs.overthewire.org -p 2220
```

Explanation:

- ssh → connect using SSH

- -i id_rsa → tells SSH to use this private key

- bandit14 → the username for the level

- …overthewire.org → the server

- -p 2220 → OTW Bandit uses port **2220**

### 4. How to Prepare the Key Before Using It

SSH requires that private keys have correct permissions:

```bash
chmod 600 id_rsa
```

If you don’t do this, SSH will reject the key as “too open”.

See more about `chmod` below.

- **Ensure Windows didn’t break the file**

The MOST common reason for “invalid format” on Windows:

- Notepad added hidden characters

- File saved as UTF‑16

- Windows line endings (CRLF)

To fix this, use **Notepad++**:

1.  Open the key

2.  Go to **Edit → EOL Conversion → Unix (LF)**

3.  Go to **Encoding → UTF‑8**

4.  Save and then try again.

### `chmod`

The Linux command used to change the permissions of a specific file.

You can change the permissions of your own files without sudo. You only need sudo permissions for files you don't own.

Here is how to read permissions and how to change them:

### 1) Reading Permission Strings

- ``ls -l`` shows a **type** + 9 permission characters: e.g., `drwxr-xr-x` see the first image at this level.

- The leading letter indicates file type (`-` file, ``d`` directory).

- Then triplets for **user**, **group**, **others** with `r` (read), `w` (write), `x` (execute), or `-` (no permission).

- Execute on a **directory** means you can *enter/traverse* it.

### 2) Changing Permission (chmod)

- **Symbolic**: target `u` (user), `g` (group), `o` (others), `a` (all);

- operation `+` add, `-` remove.  

    Examples: 
    ```bash 
    chmod u+x file
    ```
    ```bash 
    chmod g-w file
    ```
    ```bash
    chmod ug+w file
    ```

- **Octal**: `r=4`, `w=2`, `x=1`. Combine per class.

- Example: 
```bash
chmod 755 file
```
**Means:** user `rwx`, group `r-x`, others `r-x`.

- Avoid reckless recursive `777`; use ***least‑privilege***.
