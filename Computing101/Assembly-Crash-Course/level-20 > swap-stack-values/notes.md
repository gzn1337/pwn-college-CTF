# Level description



# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	push rsi
	push rdi
	push rsi
	pop rdi
	pop rsi
	pop rdi
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
- Flag received — output saved in `swap-stack-values.png`.

# Notes

this challenge we work with stack operations.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `push rsi` → pushes the original value of rsi onto the stack as temporary storage.
- `push rdi` → pushes the original value of rdi onto the stack above rsi.
- `push rsi` → pushes  rsi again on top of the stack to help with the swap.
- `pop rdi` → pops the top value (original rsi) into rdi, starting the swap.
- `pop rsi` → pops the next value (original rdi) into rsi, completing the swap.
- `pop rdi` → pops the last value (original rsi) to clean up the stack.

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

6. **Flag**: Output captured in `swap-stack-values.png`.
