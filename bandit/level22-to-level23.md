# Level 22 → Level 23

Analyze the shell script that cron executes.

> 🔗 **OverTheWire page:** [Bandit Level 22 → Level 23](https://overthewire.org/wargames/bandit/bandit23.html)

## Topics Covered

- [Reading a shell script](#step-2) → understand it line by line
- [Hashing and MD5](#what-is-hashing) → What does Hash actually mean

## Level Goal

A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

## Commands You May Need

- `cron`
- `crontab`
- `crontab(5)` (use `man 5 crontab` to access this)

## Important Notes

> **NOTE:** Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Solution

This level is a little trickier than the previous one. In [Level 21 → Level 22](./level21-to-level22.md), the script directly showed us the filename where the password was stored. Now the script **computes the filename dynamically using MD5**, so the challenge is:

*Can we understand the code well enough to predict where the password gets written?*

### Step 1

Find the cron job. Just like the previous level:

```bash
cat /etc/cron.d/cronjob_bandit23
```

Output:

```text
@reboot bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
```

What does this tell us? See the [previous level](level21-to-level22.md#a-bit-of-theory) for more details. Every minute, the script `/usr/bin/cronjob_bandit23.sh` runs as `bandit23`.

So our next target is the script:

```bash
cat /usr/bin/cronjob_bandit23.sh
```

### Step 2

Read the script. The script is:

```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

Let's break down it.

the script should be executed using Bash.

Then the command `whoami` returns the current user. For example, `bandit22` if you run it.

>But remember, the cron job is NOT running as bandit22. It's running as `bandit23`, because the cron entry says:

```text
* * * * * bandit23 ...
```

Therefore `whoami` inside the script becomes `bandit23`, so `myname="bandit23"`.

```bash
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
```

Since the `$myname` variable contains `bandit23`, the command becomes `echo I am user bandit23`, and the output is `I am user bandit23`.

That output is piped to `md5sum`:

```bash
echo I am user bandit23 | md5sum
```

Example output:

```text
8ca319486bfbbc3663ea0fbe81326349  -
```

Notice the dash at the end. To understand md5 more deeply, see the [theory below](#what-is-hashing).

Now the part `cut -d ' ' -f 1` means: the `-d` flag tells where it should split the text, which is by spaces, then take field 1.

Input:

```text
8ca319486bfbbc3663ea0fbe81326349  -
```

Output:

```text
8ca319486bfbbc3663ea0fbe81326349
```

So `mytarget="8ca319486bfbbc3663ea0fbe81326349"`.

IN simple words They create a "secret-looking" filename, `/tmp/8ca319486bfbbc3663ea0fbe81326349`, to store the password.

```bash
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
```

This only prints a status message. When executed as bandit23:

```text
Copying passwordfile /etc/bandit_pass/bandit23 to /tmp/8ca319486bfbbc3663ea0fbe81326349
```

The last line

```bash
cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

After substituting the variables:

```bash
cat /etc/bandit_pass/bandit23 > /tmp/8ca319486bfbbc3663ea0fbe81326349
```

It means: read the password that belongs to bandit23 and write it into a file located in `/tmp`.

### Step 3

How do we solve it? We need the filename. The script told us how it's generated, thankfully. We can run the same line by ourselves, but with the name `bandit23`:

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```

Output:

```text
8ca319486bfbbc3663ea0fbe81326349
```

Then we read the file with that name, which returns the password of bandit23:

```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

### Step 4

There is also an easier method. The challenge hints at it: try executing the script. Since the script is world-executable, we can run it directly:

```bash
/usr/bin/cronjob_bandit23.sh
```

It prints:

```text
Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
```

*But why does it say **bandit22** instead?*

Because we executed it as bandit22. The script uses `whoami`, which returned `bandit22`, so it calculated `md5("I am user bandit22")` instead of `md5("I am user bandit23")`.

That's why running the script manually is useful for understanding the logic, but **not** for getting the next password. The cron job executes as `bandit23`, so inside it `whoami` = `bandit23`.

## A Bit of Theory

### What is hashing?

A hash function takes any text (or file) and turns it into a fixed-length string of characters, which is called the **hash**.

>The same input always gives the same hash.
A small change in the input gives a completely different hash. Also you can't turn the hash back into the original text.

### What is MD5?

MD5 is one of the hash functions. It always gives 32 characters (hexadecimal). In Linux we can use it with the `md5sum` command:

```bash
echo "hello" | md5sum
```

Output:

```text
b1946ac92492d2347c6235b4d2611184  -
```

To remember how the pipe `|` works, see [Level 8 → Level 9](level8-to-level9.md).

> MD5 is old and it is not safe to protect passwords today. In this level it is only used to make a file name.

