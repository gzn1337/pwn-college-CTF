# Level description

In this level, you will be working with registers. You will be asked to modify or read from registers.

We will set some values in memory dynamically before each run. On each run, the values will change. This means you will need to perform some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result, which is usually rax.

It turns out that using the div operator to compute the modulo operation is slow!

We can use a math trick to optimize the modulo operator (%). Compilers use this trick a lot.

If we have x % y, and y is a power of 2, such as 2^n, the result will be the lower n bits of x.

Therefore, we can use the lower register byte access to efficiently implement modulo!

Using only the following instruction(s):

    mov

Please compute the following:

    rax = rdi % 256
    rbx = rsi % 65536

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	mov al, dil
	mov bx, si
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

Move the lower 8 bits of rdi into al and the lower 16 bits of rsi into bx to compute the modulo values.



    rdi % 256 → 256 = 100000000 in binary = 2^8 → 8 bits.
    The lower 8 bits of rdi are in dil. We need to put this in rax, but we cannot move an 8-bit register directly to a 64-bit register, so we move it to the 8-bit lower part of rax, which is al.

    rsi % 65536 → 65536 = 10000000000000000 in binary = 2^16 → 16 bits.
    The lower 16 bits of rsi are in si. We need to put this in rbx, but we cannot move a 16-bit value directly to a 64-bit register, so we move it to the 16-bit lower part of rbx, which is bx.

resulting code:

```asm
mov al, dil
mov bx, si
```

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.


2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov al, dil` → move the lower 8 bits of rdi into the lower 8 bits of rax (al), computing rdi % 256.
- `mov bx, si` → move the lower 16 bits of rsi into the lower 16 bits of rbx (bx), computing rsi % 65536.


3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.


4. **Link**: `ld solution.o -o solution` produces the final executable.


5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

