# PwnCollege — Cybersecurity Notes & Solutions

This repository documents my journey through the **PwnCollege** challenges.  
It is a collection of solutions, structured notes, and references aimed at learning and sharing practical cybersecurity knowledge.

---

## 📂 Repository Structure (recommended)
```
pwncollege-ctf/
├─ README.md               # <- this file
├─ assembly/               # Low-level Assembly Crash Course notes
│  ├─ 01-registers/
│  │  ├─ solution.asm
│  │  ├─ notes.md
│  │  └─ screenshots/
│  └─ ...
├─ exploitation/           # Binary exploitation challenges
├─ reversing/              # Reverse engineering challenges
├─ crypto/                 # Cryptography challenges
├─ web/                    # Web security challenges
├─ forensics/              # Forensics / misc challenges
└─ resources/              # Cheatsheets, tools and reference links
```

Each challenge folder should contain:
- `solution.*` files (e.g., `solution.asm`, `exploit.py`, etc.)  
- `notes.md` — clear walkthrough and explanations  
- optional `screenshots/` with outputs or flags

---

## 🧭 Goals
- Document solutions to **learn deeply** from each challenge.  
- Build a practical **knowledge base** covering:  
  - Assembly & system calls  
  - Binary exploitation (ROP, format strings, heap)  
  - Reverse engineering  
  - Cryptography  
  - Web vulnerabilities  
  - Forensics & misc topics  
- Produce clear, reproducible write-ups that help others learn.

---

## 🚀 How to Use
1. Enter a challenge folder.  
2. Read `notes.md` for the walkthrough and rationale.  
3. Build and run the provided solution following the instructions in the notes.

Example (Assembly / 64-bit Linux):
```bash
nasm -f elf64 solution.asm -o solution.o
ld solution.o -o solution
/challenge/run /home/hacker/solution
```

> If the challenge requires the program to exit without altering important registers, check the notes for an adjusted exit/syscall that preserves the required register values.

---

## 🛠️ Common Tools & References
- **Binary exploitation**: `gdb`, `pwntools`, `gef`, `radare2`  
- **Reversing**: `ghidra`, `IDA Free`, `objdump`, `strings`  
- **Crypto**: Python, `sage`, `hashcat`  
- **Web**: `Burp Suite`, browser dev tools, curl  
- **General**: `nasm`, `ld`, Linux CLI, Python

Useful cheatsheets and commands should live in `resources/cheatsheet.md`.

---

## 🧩 Naming & Contribution Conventions
- Level folders: `NN-category-shortname` (e.g., `01-assembly-registers`, `05-bof-basic`).  
- `notes.md` structure: `Level description`, `Solution`, `Notes/Observations`.  
- Use uppercase register names and `0x` prefix for hex values (e.g., `RAX = 0x1337`).  
- Commit message examples:
  - `add: 01-assembly-registers solution and notes`
  - `fix: typo in notes.md`

Contributions, suggestions, and PRs are welcome. If you add a new level, follow the folder and notes conventions.

---

## 📜 License
Suggested license: **MIT** — feel free to reuse or adapt this content for learning and sharing.

---

## 🌟 Final Notes
This repo is a learning log and practical cybersecurity reference. It will grow as I progress through PwnCollege and other CTFs.  
Feedback, questions, and pull requests are welcome — let's learn together.
