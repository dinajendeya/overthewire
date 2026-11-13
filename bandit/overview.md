# Bandit Level 0 – Before We Start

Hi cybersecurity enthusiast. If you are interested in learning cybersecurity, you will definitely hear about OTW. In this room we will answer a few important questions before we start the walkthrough of each level.

1. What is OverTheWire?
2. How does OTW work and how to start using it step by step?
3. A bit of theory: what is SSH, and why does Bandit use port 2220? See [Level 0](level0.md#a-bit-of-theory).

## What is OverTheWire?

OTW is a great place to start your cybersecurity journey. It teaches you cybersecurity concepts through hands-on, beginner-friendly war game challenges. It's the best place to apply your cybersecurity knowledge to the real-world experience that hackers face day to day.

OTW is divided into games, where each game focuses on a specific topic:

- Bandit
- ...

## How Does OTW Work?

OTW provides several war games that contain many levels. You solve the level by finding out the password to log in to the next one, applying essential cybersecurity skills. If you struggle to pass a level, you can't move on or jump up levels. Never give up, keep trying and learning new concepts through your journey. This is what really matters here.

Read other people's write-ups, including this blog, and notice how they approach challenges and learn their mindset. No copy and paste! No password stealing.

You solve the level → get the password → use it to log into the next account.

## How to Start Using OverTheWire

### 1️. Go to the official website

 [https://overthewire.org](https://overthewire.org/)

Then click **"Wargames"** → choose **Bandit**.

### 2️. Learn how to connect via SSH

Each level is a remote Linux machine you log into. You should use the credentials in the top corner and log in using the SSH protocol.

If this is the first time you hear about the SSH protocol, see [Level 0](level0.md).

For example, to start Bandit, in your terminal:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

- `bandit0` → username
- `bandit.labs.overthewire.org` → hostname
- `-p 2220` → the port number

### 3️. Solve each level by using Linux commands

Example: Level 0 → find a file in the home directory and read its content:

```bash
ls
cat readme
```

The output is the password for level 1.

### 4️. Use that password to log into the next level

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Don't forget to save the password you found, so you can log in whenever you want.

Or use the `ssh bandit2@localhost -p 2220` command while you are logged in as a bandit user and you are already on the OverTheWire server.

### Repeat this for every level

Each level = new user = new password.
