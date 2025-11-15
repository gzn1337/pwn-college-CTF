# Level description

In this level, you will be working with registers. You will be asked to modify or read from registers.

We will set some values in memory dynamically before each run. On each run, the values will change. This means you will need to perform some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result, which is usually rax.

In this level, you will be working with bit logic and operations. This will involve heavy use of directly interacting with bits stored in a register or memory location. You will also likely need to make use of the logic instructions in x86: and, or, not, xor.

Shifting bits around in assembly is another interesting concept!

x86 allows you to 'shift' bits around in a register.

Take, for instance, al, the lowest 8 (or least significant 8) bits of rax.

The value in al (in bits) is:

rax = 10001010

If we shift once to the left using the shl instruction:

shl al, 1

The new value is:

al = 00010100

Everything shifted to the left, and the highest (or most significant) bit fell off while a new 0 was added to the right side.

You can use this to do special things to the bits you care about.

Shifting has the nice side effect of doing quick multiplication (by 2) or division (by 2), and can also be used to compute modulo.

Here are the important instructions:

    shl reg1, reg2 <=> Shift reg1 left by the amount in reg2
    shr reg1, reg2 <=> Shift reg1 right by the amount in reg2

Note: 'reg2' can be replaced by a constant or memory location.

When we say significant bit or least significant byte, significant means "most important for the value."

    The least significant bit/byte carries the smallest weight (the "lowest" place value). For example, when you modify the "lowest" or "rightmost" bit, the value changes just by 1.
    The most significant bit/byte carries the highest weight (the "highest" place value).

For this challenge, using only the following instructions:

    mov, shr, shl

Please perform the following: Set rax to the 5th least significant byte of rdi.

For example:

rdi = | B7 | B6 | B5 | B4 | B3 | B2 | B1 | B0 |
Set rax to the value of B4


# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	shr rdi, 32
	mov al, dil
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

first we shift right 32 bytes in rdi, to put the 5th byte (B4) to (B0, least significant byte). After that we just move this to rax 8 bits register (al).

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `shr rdi, 32` → shift **rdi** right by 32 bits to bring the 5th least significant byte (B4) down to the lowest byte position.
- `mov al, dil` → move the lowet 8 bits of **rdi** (dil) into the lowest 8 bits of **rax** (al).

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

