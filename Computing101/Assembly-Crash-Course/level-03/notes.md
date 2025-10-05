# Level description

In this level, you will be working with registers. 
You will be asked to modify or read from registers.

We will set some values in memory dynamically before each run. 
On each run, the values will change.

This means you will need to perform some formulaic operation with registers. 
We will tell you which registers are set beforehand and where you should put the result. 
In most cases, it's **rax**.

Many instructions exist in x86 that allow you to perform all the normal math operations on registers and memory.

For shorthand, when we say A += B, it really means A = A + B.

Here are some useful instructions:

- add reg1, reg2 <=> reg1 += reg2
- sub reg1, reg2 <=> reg1 -= reg2
- imul reg1, reg2 <=> reg1 *= reg2

**div** is more complicated, and we will discuss it later. Note: all **regX** can be replaced by a constant or memory location.

Do the following:

* Add **0x331337** to **rdi**

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	add rdi, 0x331337
```
3. Assemble:
```bash
nasm -f elf64 solution.asm -o solution.o
```

4. Link:
```bash
ld solution.o -o solution
```

5. Run the challenge:
```bash
/challenge/run /home/hacker/solution
```

6. Result:
- Flag received — output saved in `level-3.png`.

# Notes

In the level description, we can see useful instructions to some math operations,
which help us to create or assembly file correctly, just adding 0x331337 to the **rdi** with **add**.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` -> declares the entry point for the linker.
- `_start:` -> line where execution begins.
- `add rdi, 0x331337` -> adds 0x331337 to **rdi** register.

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

6. **Flag**: Output captured in `level-3.png`.
