# Level description

In this level, you will be working with registers. You will be asked to modify or read from registers.

We will set some values in memory dynamically before each run. On each run, the values will change. This means you will need to perform some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result, which is usually rax.

Division in x86 is more special than in normal math. Math here is called integer math, meaning every value is a whole number.

As an example: 10 / 3 = 3 in integer math.

Why?

Because 3.33 is rounded down to an integer.

The relevant instructions for this level are:

    mov rax, reg1
    div reg2

Note: div is a special instruction that can divide a 128-bit dividend by a 64-bit divisor while storing both the quotient and the remainder, using only one register as an operand.

How does this complex div instruction work and operate on a 128-bit dividend (which is twice as large as a register)?

For the instruction div reg, the following happens:

    rax = rdx:rax / reg
    rdx = remainder

rdx:rax means that rdx will be the upper 64-bits of the 128-bit dividend and rax will be the lower 64-bits of the 128-bit dividend.

You must be careful about what is in rdx and rax before you call div.

Please compute the following:

    speed = distance / time, where:
        distance = rdi
        time = rsi
        speed = rax

Note that distance will be at most a 64-bit value, so rdx should be 0 when dividing.

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:
	mov rax, rdi
	div rsi
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
- Flag received — output saved in `level-5.png`.

# Notes

Simple challenge, just a simple math operation, takes more time to read the description than writing the code.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov rax, rdi` -> moving **rdi** to **rax** -- speed(rax) = distance(rdi)
- `div rsi` -> divide the 128-bit value in rdx:rax by **rsi**, storing the quotient in **rax** and the remainder in **rdx**
3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

6. **Flag**: Output captured in `level-5.png`.
