# Level description

In this level, you will be working with registers. You will be asked to modify or read from registers.

We will set some values in memory dynamically before each run. On each run, the values will change. This means you will need to perform some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result, which is usually rax.

In this level, you will be working with bit logic and operations. This will involve heavy use of directly interacting with bits stored in a register or memory location. You will also likely need to make use of the logic instructions in x86: and, or, not, xor.

Bitwise logic in assembly is yet another interesting concept! x86 allows you to perform logic operations bit by bit on registers.

For the sake of this example, say registers only store 8 bits.

The values in rax and rbx are:

    rax = 10101010
    rbx = 00110011

If we were to perform a bitwise AND of rax and rbx using the and rax, rbx instruction, the result would be calculated by ANDing each bit pair one by one, hence why it's called bitwise logic.

So from left to right:

    1 AND 0 = 0
    0 AND 0 = 0
    1 AND 1 = 1
    0 AND 1 = 0
    ...

Finally, we combine the results together to get:

    rax = 00100010

Here are some truth tables for reference:

    AND

    A | B | X
    ---+---+---
    0 | 0 | 0
    0 | 1 | 0
    1 | 0 | 0
    1 | 1 | 1

    OR

    A | B | X
    ---+---+---
    0 | 0 | 0
    0 | 1 | 1
    1 | 0 | 1
    1 | 1 | 1

    XOR

    A | B | X
    ---+---+---
    0 | 0 | 0
    0 | 1 | 1
    1 | 0 | 1
    1 | 1 | 0

Without using the following instructions: mov, xchg

Please perform the following:

Set rax to the value of (rdi AND rsi)

NOTE: rax will have all bits set to 1 If it didn't, this level would be trickier!

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	and rdi, rsi
	and rax, rdi
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

# Notes

here we perform a **bitwise** AND between **rdi** and **rsi**, setting rax to 1 only where both corresponding bits are 1.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `and rdi, rsi` → perform a bitwise AND between rdi and rsi, storing the result in rdi.
- `and rax, rdi` → perform a bitwise AND between rax and rdi, storing the result in rax.

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.
