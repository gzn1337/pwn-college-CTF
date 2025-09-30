# Level description

In this level, you will be working with registers. You will be asked to modify or read from registers.

We will set some values in memory dynamically before each run. On each run, the values will change. This means you will need to perform some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result, which is usually rax.

This means you will need to perform a formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

Modulo in assembly is another interesting concept!

x86 allows you to get the remainder after a div operation.

For instance: 10 / 3 results in a remainder of 1.

The remainder is the same as modulo, which is also called the "mod" operator.

In most programming languages, we refer to mod with the symbol %.

Please compute the following: rdi % rsi

Place the value in rax.

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
- Flag received — output saved in `level-6.png`.

# Notes

this level is like the last one (level-5), but here we wanted the remainder instead of the quotient.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov rax, rdi` -> move dividend into **rax**
- `div rsi` -> (rdx:rax) / rsi
- `mov rax, rdx` -> move the remainder(mod) into **rax**
3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

6. **Flag**: Output captured in `level-6.png`.
