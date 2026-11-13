<h1 align="center">OverTheWire Writeups</h1>

<p align="center">
  <img alt="Wargames" src="https://img.shields.io/badge/OverTheWire-Wargames-blue">
  <img alt="Bandit" src="https://img.shields.io/badge/Bandit-completed-brightgreen">
  <img alt="Natas" src="https://img.shields.io/badge/Natas-coming%20soon-lightgrey">
  <img alt="Leviathan" src="https://img.shields.io/badge/Leviathan-coming%20soon-lightgrey">
  <img alt="Topic" src="https://img.shields.io/badge/topic-cybersecurity-red">
  <img alt="Purpose" src="https://img.shields.io/badge/purpose-educational-green">
</p>

# OverTheWire Writeups

My personal learning journey through the [OverTheWire](https://overthewire.org/wargames/) wargames. Every write-up explains the level step by step, with screenshots, links to the official level page, and a bit of theory about the new topics used in the level.

## Table of Contents

- [Games](#games)
- [Bandit](#bandit)
  - [All Bandit levels](#all-bandit-levels)
- [Natas](#natas)
- [Leviathan](#leviathan)
- [Repository Structure](#repository-structure)
- [Progress Tracker](#progress-tracker)
- [Disclaimer](#disclaimer)

## Games

| Game | Focus | Write-ups | Official page | Status |
|------|-------|-----------|---------------|--------|
| **Bandit** | Linux command line, SSH, networking basics, cron and git | [bandit/](bandit/) | [overthewire.org/wargames/bandit](https://overthewire.org/wargames/bandit/) | ✅ Completed |
| **Natas** | Web security | [natas/](natas/) | [overthewire.org/wargames/natas](https://overthewire.org/wargames/natas/) | ⚪ Coming soon |
| **Leviathan** | Basic binary exploitation and Linux tricks | [leviathan/](leviathan/) | [overthewire.org/wargames/leviathan](https://overthewire.org/wargames/leviathan/) | ⚪ Coming soon |

## Bandit

Bandit is the first wargame, made for absolute beginners. It teaches the basics we need to play the other wargames.

**Start here:**

- [Bandit overview](bandit/overview.md): what OverTheWire is and how to start
- [Level 0](bandit/level0.md): how to connect to the server with SSH

Every walkthrough has the same structure:

1. A link to the **official OverTheWire level page**
2. **Topics Covered**: a quick reference to the new topics explained in the level (each one links to its theory)
3. **Level Goal** and **Commands You May Need**
4. **Solution** step by step, with screenshots
5. **A Bit of Theory**

### All Bandit Levels

| Level | Walkthrough | Topics | OverTheWire |
|-------|-------------|--------|-------------|
| 0→1 | [Level 0 → Level 1](bandit/level0-to-level1.md) | `ls` and `cat` · Home directory | [Official](https://overthewire.org/wargames/bandit/bandit1.html) |
| 1→2 | [Level 1 → Level 2](bandit/level1-to-level2.md) | Flags · Dashed file names | [Official](https://overthewire.org/wargames/bandit/bandit2.html) |
| 2→3 | [Level 2 → Level 3](bandit/level2-to-level3.md) | Spaces in file names | [Official](https://overthewire.org/wargames/bandit/bandit3.html) |
| 3→4 | [Level 3 → Level 4](bandit/level3-to-level4.md) | Hidden files · Paths | [Official](https://overthewire.org/wargames/bandit/bandit4.html) |
| 4→5 | [Level 4 → Level 5](bandit/level4-to-level5.md) | Human-readable files | [Official](https://overthewire.org/wargames/bandit/bandit5.html) |
| 5→6 | [Level 5 → Level 6](bandit/level5-to-level6-add-permession-level.md) | `find` command | [Official](https://overthewire.org/wargames/bandit/bandit6.html) |
| 6→7 | [Level 6 → Level 7](bandit/level6-to-level7.md) | File descriptors · Redirecting errors | [Official](https://overthewire.org/wargames/bandit/bandit7.html) |
| 7→8 | [Level 7 → Level 8](bandit/level7-to-level8.md) | `grep` | [Official](https://overthewire.org/wargames/bandit/bandit8.html) |
| 8→9 | [Level 8 → Level 9](bandit/level8-to-level9.md) | `sort` and `uniq` · Pipe `\|` | [Official](https://overthewire.org/wargames/bandit/bandit9.html) |
| 9→10 | [Level 9 → Level 10](bandit/level9-to-level10.md) | `strings` | [Official](https://overthewire.org/wargames/bandit/bandit10.html) |
| 10→11 | [Level 10 → Level 11](bandit/level10-to-level11.md) | Base64 · Encoding vs encryption | [Official](https://overthewire.org/wargames/bandit/bandit11.html) |
| 11→12 | [Level 11 → Level 12](bandit/level11-to-level12.md) | ROT13 and the Caesar cipher · `tr` command | [Official](https://overthewire.org/wargames/bandit/bandit12.html) |
| 12→13 | [Level 12 → Level 13](bandit/level12-to-level13.md) | Hexdump · `mktemp` · Compression and archives | [Official](https://overthewire.org/wargames/bandit/bandit13.html) |
| 13→14 | [Level 13 → Level 14](bandit/level13-to-level14.md) | Private SSH key · `chmod` | [Official](https://overthewire.org/wargames/bandit/bandit14.html) |
| 14→15 | [Level 14 → Level 15](bandit/level14-to-level15.md) | Ports · Netcat (`nc`) | [Official](https://overthewire.org/wargames/bandit/bandit15.html) |
| 15→16 | [Level 15 → Level 16](bandit/level15-to-level16.md) | SSL/TLS · `openssl s_client` | [Official](https://overthewire.org/wargames/bandit/bandit16.html) |
| 16→17 | [Level 16 → Level 17](bandit/level16-to-level17.md) | Nmap · KeyUpdate message | [Official](https://overthewire.org/wargames/bandit/bandit17.html) |
| 17→18 | [Level 17 → Level 18](bandit/level17-to-level18.md) | `diff` | [Official](https://overthewire.org/wargames/bandit/bandit18.html) |
| 18→19 | [Level 18 → Level 19](bandit/level18-to-level19.md) | Running a command through `ssh` | [Official](https://overthewire.org/wargames/bandit/bandit19.html) |
| 19→20 | [Level 19 → Level 20](bandit/level19-to-level20.md) | setuid and setgid | [Official](https://overthewire.org/wargames/bandit/bandit20.html) |
| 20→21 | [Level 20 → Level 21](bandit/level20-to-level21.md) | Netcat listener · setuid network client | [Official](https://overthewire.org/wargames/bandit/bandit21.html) |
| 21→22 | [Level 21 → Level 22](bandit/level21-to-level22.md) | Cron jobs · Cron schedule · Shebang | [Official](https://overthewire.org/wargames/bandit/bandit22.html) |
| 22→23 | [Level 22 → Level 23](bandit/level22-to-level23.md) | Reading a shell script · Hashing and MD5 | [Official](https://overthewire.org/wargames/bandit/bandit23.html) |
| 23→24 | [Level 23 → Level 24](bandit/level23-to-level24.md) | Writing your first shell script · Commands inside the script | [Official](https://overthewire.org/wargames/bandit/bandit24.html) |
| 24→25 | [Level 24 → Level 25](bandit/level24-to-level25.md) | Brute forcing · Sockets in Python | [Official](https://overthewire.org/wargames/bandit/bandit25.html) |
| 25→26 | [Level 25 → Level 26](bandit/level25-to-level26.md) | Default shell of a user · `more` and `vim` | [Official](https://overthewire.org/wargames/bandit/bandit26.html) |
| 26→27 | [Level 26 → Level 27](bandit/level26-to-level27.md) | Shell escape from vim · setuid binary | [Official](https://overthewire.org/wargames/bandit/bandit27.html) |
| 27→28 | [Level 27 → Level 28](bandit/level27-to-level28.md) | Git and `git clone` · Why `/tmp` | [Official](https://overthewire.org/wargames/bandit/bandit28.html) |
| 28→29 | [Level 28 → Level 29](bandit/level28-to-level29.md) | Commits and history · `git log` and `git show` | [Official](https://overthewire.org/wargames/bandit/bandit29.html) |
| 29→30 | [Level 29 → Level 30](bandit/level29-to-level30.md) | Branches · `git branch -a` and `git checkout` | [Official](https://overthewire.org/wargames/bandit/bandit30.html) |
| 30→31 | [Level 30 → Level 31](bandit/level30-to-level31.md) | Git tags | [Official](https://overthewire.org/wargames/bandit/bandit31.html) |
| 31→32 | [Level 31 → Level 32](bandit/level31-to-level32.md) | `.gitignore` · `git add -f`, commit and push | [Official](https://overthewire.org/wargames/bandit/bandit32.html) |
| 32→33 | [Level 32 → Level 33](bandit/level32-to-level33.md) | `$0` shell escape | [Official](https://overthewire.org/wargames/bandit/bandit33.html) |
| 33→34 | [Level 33 → Level 34](bandit/level33-to-level34.md) | End of Bandit | [Official](https://overthewire.org/wargames/bandit/bandit34.html) |

## Natas

Write-ups will be added in [natas/](natas/). Official page: [OverTheWire Natas](https://overthewire.org/wargames/natas/).

## Leviathan

Write-ups will be added in [leviathan/](leviathan/). Official page: [OverTheWire Leviathan](https://overthewire.org/wargames/leviathan/).

## Repository Structure

```text
.
├── README.md
├── assets/        screenshots, one folder per game and level
│   ├── bandit/
│   ├── natas/
│   └── leviathan/
├── bandit/        Bandit level write-ups
├── natas/         Natas write-ups
└── leviathan/     Leviathan write-ups
```

Screenshots are saved in `assets/<game>/level<N>/` for the level `N → N+1` and named in order, for example `assets/bandit/level26/03-vim-set-shell.png`.

## Progress Tracker

| Game | Write-ups | Status |
|------|-----------|--------|
| [Bandit](#bandit) | 34 levels (0 → 34) | ✅ Completed |
| [Natas](#natas) | 0 | ⚪ Not started |
| [Leviathan](#leviathan) | 0 | ⚪ Not started |

## Disclaimer

This repository is for **educational purposes only**. All challenges are intentionally built for learning on the OverTheWire platform. Try each level yourself first, and use these write-ups to understand the ideas, not to copy answers.
