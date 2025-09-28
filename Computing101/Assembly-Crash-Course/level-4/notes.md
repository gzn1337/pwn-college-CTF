# Level description

In this level, you will be working with registers. 
You will be asked to modify or read from registers.

We will now set some values in memory dynamically before each run. On each run, the values will change. This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

Using your new knowledge, please compute the following:

    f(x) = mx + b, where:
        m = rdi
        x = rsi
        b = rdx

Place the result into rax.

Note: There is an important difference between mul (unsigned multiply) and imul (signed multiply) in terms of which registers are used. Look at the documentation on these instructions to see the difference.

In this case, you will want to use imul.

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```bash
global _start

_start:

	imul rdi, rsi
	add rdx, rdi
	mov rax, rdx
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
- Flag received — output saved in `level-4.png`.

# Notes

In this challenge, we use a linear equation formula
which is in the level description:
**f(x) = mx + b**
this in code must be:

rdi = m * x
rdx = b + (m*x)
rax = f(x) = m*x + b 

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` -> declares the entry point for the linker.
- `_start:` -> line where execution begins.
- `imul rdi, rsi` -> multiply **rdi** (m) by **rsi** (x).
- `add rdx, rdi` -> add the multiplication result in **rdi** to **rdx**(b).
- `mov rax, rdx` -> moving the result to **rax** register as requested.
3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

6. **Flag**: Output captured in `level-4.png`.
