# Lab 2 — Version Control & Advanced Git

## Task 1 — Git Object Model Exploration

### Outputs

* blob
	```bash
	$ git cat-file -p 6e60bebec0724892a7c82c52183d0a7b467cb6bb
	# 🚀 DevOps Introduction Course: Principles, Practices & Tooling

	[![Labs](https://img.shields.io/badge/Labs-80%25-blue)](#-lab-based-learning-experience)
	[![Exam](https://img.shields.io/badge/Exam-20%25-orange)](#-evaluation-framework)
	[![Hands-On](https://img.shields.io/badge/Focus-Hands--On%20Labs-success)](#-lab-based-learning-experience)
	[![Duration](https://img.shields.io/badge/Duration-10%20Weeks-lightgrey)](#-course-roadmap)

	Welcome to the **DevOps Introduction Course**, where you will gain a **solid foundation in DevOps principles and practical skills**.
	This course is designed to provide a comprehensive understanding of DevOps and its key components.
	...

	Source: lectures/lec1.md

	- 📍 Slide 1 – 🚀 What is DevOps?
	- 📍 Slide 2 – 📜 A Brief History of DevOps
	- 📍 Slide 3 – 🎯 Why DevOps? (Key Goals)
	- 📍 Slide 4 – ⚖️ DevOps vs. Traditional IT
	...

	Source: lectures/lec2.md

	- 📍 Slide 1 – 🧭 What is a Version Control System (VCS)?
	- 📍 Slide 2 – 🔎 Why We Need Version Control
	- 📍 Slide 3 – 🕰️ A Short History of VCS (to Understand Today)
	- 📍 Slide 4 – 🧭 Centralized vs Distributed VCS
	...

	Source: lectures/lec3.md

	- 📍 Slide 1 – 🌍 What is CI/CD?
	- 📍 Slide 2 – 🕰️ Short History of CI/CD
	- 📍 Slide 3 – 📈 Why CI/CD Matters
	- 📍 Slide 4 – 🏗️ Core Principles of Continuous Integration
	...

	Source: lectures/lec4.md

	- 📍 Slide 1 – 🌐 Introduction to Networking in DevOps
	- 📍 Slide 2 – 📡 OSI Model & TCP/IP Stack
	- 📍 Slide 3 – 🔢 IP Addressing & Subnetting
	- 📍 Slide 4 – 🌐 DNS (Domain Name System)
	...

	Source: lectures/lec5.md

	- 📍 Slide 1 – 🌟 Introduction to Virtualization - What & Why
	- 📍 Slide 2 – 📚 History of Virtualization (1960s IBM Mainframes → Modern Cloud)
	- 📍 Slide 3 – 💡 Core Concepts - Physical vs Virtual Resources
	- 📍 Slide 4 – 🎯 Benefits of Virtualization (Cost, Efficiency, Flexibility)
	...

	Source: lectures/lec6.md

	- 📍 Slide 1 – 🐳 What are Containers?
	- 📍 Slide 2 – 📜 History of Containers (1979 → 2024)
	- 📍 Slide 3 – 💡 Why Containers Matter in DevOps
	- 📍 Slide 4 – ⚖️ Containers vs Virtual Machines (VMs)
	...

	Source: lectures/lec7.md

	- 📍 Slide 1 – 🚀 What is GitOps? - The Modern Way to Operate
	- 📍 Slide 2 – 📜 GitOps History - From FTP to Pull Requests
	- 📍 Slide 3 – 🎯 GitOps Principles - The Four Golden Rules
	- 📍 Slide 4 – ⚡ Push vs Pull Deployment Models - The Great Debate
	...

	Source: lectures/lec8.md

	- 📍 Slide 1 – 🛡️ What is SRE? - Engineering Approach to Operations
	- 📍 Slide 2 – 📜 History of SRE - From Google's Need to Industry Standard
	- 📍 Slide 3 – 🤝 SRE vs DevOps vs Platform Engineering - Clarifying the Roles
	- 📍 Slide 4 – 🎨 SRE Principles - Reliability, Scalability, and Toil Reduction
	...

	Source: lectures/lec9.md

	- 📍 Slide 1 – 🛡️ What is DevSecOps? - Security as Code
	- 📍 Slide 2 – 📜 History of DevSecOps - From Afterthought to Built-in
	- 📍 Slide 3 – 🎯 Why DevSecOps Matters - The Security Crisis
	- 📍 Slide 4 – 🔑 Core DevSecOps Principles - The Security Mindset
	...
	Source: lectures/lec10.md

	- 📍 Slide 1 – ☁️ Cloud Computing Overview
	- 📍 Slide 2 – 🖥️ Compute Services - VMs
	- 📍 Slide 3 – 📦 Compute Services - Containers
	- 📍 Slide 4 – ⚡ Compute Services - Serverless
	...

	---

	## 🗺️ DevOps Learning Journey

	<details>
	<summary>🌳 View Skill Tree Structure</summary>
	...
	```

* tree
	```bash
	$ git cat-file -p 9f87a5d504773c42a7ade47077dc2326f3b36364
	040000 tree d717a24b35173244f4285884956c387c6f7bc816    .github
	100644 blob 6e60bebec0724892a7c82c52183d0a7b467cb6bb    README.md
	040000 tree a1061247fd38ef2a568735939f86af7b1000f83c    app
	040000 tree 6d6220700a2e7901129edcab8bd4bd35344a8e13    labs
	040000 tree d3fb3722b7a867a83efde73c57c49b5ab3e62c63    lectures
	```

* commit_hash
	```bash
	$ git cat-file -p c6a700d
	tree 9f87a5d504773c42a7ade47077dc2326f3b36364
	parent b268b8d54b2fd365c1b8be481f374b40451c31ac
	author scrii <en3rgy.channel4@gmail.com> 1770993534 +0300
	committer scrii <en3rgy.channel4@gmail.com> 1770993534 +0300
	gpgsig -----BEGIN SSH SIGNATURE-----
	 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgYpSu2zegQ/DflAE4oTqgeXd3G4
	 oQIJb1OT2XYEVhzAEAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
	 AAAAQNdGGbFDOJ6Sw1jYb944bZLb1VIVlS3UgxI4LgsBQwJNMzv0fToGgdIP3yE39Sf8og
	 19rf/5LhjA8JZ30ctVPwQ=
	 -----END SSH SIGNATURE-----

	Add test file
	```

### Contents

* **blob**: Stores the contents of a file (the text of `README.md`)

* **tree**: Represents a directory mapping filenames to the corresponding blobs or subtrees.

* **commit**: A snapshot of the repository.

### Git Repo Data Storage Analysis

Git contains data as key-value pairs, where `blob` (binary large object) is a file content itself w/o metadata, `tree` contains the links to other `trees` and `blobs`, `commit` stores the metadata and the root `tree`.

### Examples

The examples are provided in the `ouputs` section.


## Task 2 — Reset and Reflog Recovery

### The Commands I Ran
* Logs after commiting the test files:

	```bash
	$ git log

	commit df37f6800b0f7ae0675258c12d9335fcc0738aa0 (HEAD -> git-reset-practice)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:17 2026 +0300

	    Third commit

	commit 0ce8fb5b7c50e9a4fc4d1dca0c5cbf713baa6670
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:16 2026 +0300

	    Second commit

	commit fda3eba6afe2410a203791dd968d9f4b4a1f6e27
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:16 2026 +0300

	    First commit

	commit c6a700dc96143c840b3aa97c35c759cf3543f941 (feature/lab2)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 17:38:54 2026 +0300

	    Add test file
	commit df37f6800b0f7ae0675258c12d9335fcc0738aa0 (HEAD -> git-reset-practice)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:17 2026 +0300
	```

* Make soft reset

	```bash
	$ git reset --soft HEAD~1
	$ git log

	commit 0ce8fb5b7c50e9a4fc4d1dca0c5cbf713baa6670 (HEAD -> git-reset-practice)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:16 2026 +0300

	    Second commit

	commit fda3eba6afe2410a203791dd968d9f4b4a1f6e27
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:16 2026 +0300

	    First commit

	commit c6a700dc96143c840b3aa97c35c759cf3543f941 (feature/lab2)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 17:38:54 2026 +0300

	    Add test file

	commit b268b8d54b2fd365c1b8be481f374b40451c31ac (origin/feature/lab1, feature/lab1)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 6 17:58:24 2026 +0300
	```
	The branch pointer moved to the parent commit `0ce8fb5`, `df37f68` is no longer reachable, but still exists. The index and the working tree are unchanged.

* Make hard reset

	```bash
	$ git reset --hard HEAD~1
	$ git log

	commit fda3eba6afe2410a203791dd968d9f4b4a1f6e27 (HEAD -> git-reset-practice)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:16 2026 +0300

	    First commit

	commit c6a700dc96143c840b3aa97c35c759cf3543f941 (feature/lab2)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 17:38:54 2026 +0300

	    Add test file

	commit b268b8d54b2fd365c1b8be481f374b40451c31ac (origin/feature/lab1, feature/lab1)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 6 17:58:24 2026 +0300

	    docs: update

	commit 8bdffbe343a74bed3966c4baf2357432884232c1
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 6 17:53:27 2026 +0300
	```
	The branch pointer moves to the parent of the current HEAD (`0ce8fb5` -> `fda3eba`). The index now matches the `First Commit`. The working tree is overwritten to the state of the `First Commit`.


* Looking for the made changes
	```bash
	$ git reflog

	fda3eba (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
	0ce8fb5 HEAD@{1}: reset: moving to HEAD~1
	df37f68 HEAD@{2}: commit: Third commit
	0ce8fb5 HEAD@{3}: commit: Second commit
	fda3eba (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
	c6a700d (feature/lab2) HEAD@{5}: checkout: moving from feature/lab2 to git-reset-practice
	c6a700d (feature/lab2) HEAD@{6}: commit: Add test file
	...
	```

* Cancelling all the manipulations and returning to the `Third Commit` commit

	```bash
	$ git reset --hard df37f68
	HEAD is now at df37f68 Third commit

	$ git log

	commit df37f6800b0f7ae0675258c12d9335fcc0738aa0 (HEAD -> git-reset-practice)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:17 2026 +0300

	    Third commit

	commit 0ce8fb5b7c50e9a4fc4d1dca0c5cbf713baa6670
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:16 2026 +0300

	    Second commit

	commit fda3eba6afe2410a203791dd968d9f4b4a1f6e27
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 18:10:16 2026 +0300

	    First commit

	commit c6a700dc96143c840b3aa97c35c759cf3543f941 (feature/lab2)
	Author: scrii <en3rgy.channel4@gmail.com>
	Date:   Fri Feb 13 17:38:54 2026 +0300
	```
	The branch pointer is moved to the `Third Commit`. The resets are cancelled, and the branch history is restored to its original state. The index now corresponds to the `Third Commit`. The working tree is overwritten: the files are restored to the content of the `Third Commit`.

	By looking on the changes of the HEAD position via `reflog`, the changes were cancelled by finding the desired commit (in this case the `Third Commit`).


## Task 3 — Visualize Commit History

### The Graph And the Commit messages

```bash
$ git log --oneline --graph --all
* fd69ee4 (side-branch) Side branch commit
| * 8f862fd (git-reset-practice) Side branch commit
| * df37f68 Third commit
| * 0ce8fb5 Second commit
| * fda3eba First commit
|/
```

The graph shows the current branches history and their commits allowing to understand the current state of the development.


## Task 4 — Tagging Commits

```bash
$ git log

commit c6a700dc96143c840b3aa97c35c759cf3543f941 (HEAD -> feature/lab2, tag: v1.0.0)
Author: scrii <en3rgy.channel4@gmail.com>
Date:   Fri Feb 13 17:38:54 2026 +0300

    Add test file
...
```

The tag name is `tag: v1.0.0`its associated is `c6a700`.
Tags identify the release points and used as CI/CD triggers allowing to provide the release notes.


## Task 5 — Git Switch vs Git Checkout vs Git Restore

### Logs And Outputs

```bash
$ git switch -c cmd-compare
Switched to a new branch 'cmd-compare'

$ git status
On branch cmd-compare
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        demo.txt
        submission2.md

$ git switch -
Switched to branch 'feature/lab2'

$ git branch
* cmd-compare
  feature/lab1
  feature/lab2
  git-reset-practice
  main
  side-branch

```

Use for creating new branch and automatically switching:

```bash
$ git switch -c <branch_name>
```

Use for showing the existing branches:
```bash
$ git branch
```

## Task 6 — GitHub Community Engagement

 This actions are useful to provide the feedback on authors works. Starring shows engagement of the users allowing to estimate the usability and usefulness of the repos. On the other hand, it is a sign for the authors that motivates them to contribute more on the starred projects.
 
