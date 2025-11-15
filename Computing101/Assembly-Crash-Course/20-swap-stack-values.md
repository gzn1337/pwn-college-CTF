# Level description

We will now set some values in memory dynamically before each run. On each run the values will change. This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

In this level, you will be working with the stack, the memory region that dynamically expands and shrinks. You will be required to read and write to the stack, which may require you to use the pop and push instructions. You may also need to use the stack pointer register (rsp) to know where the stack is pointing.

In this level, we are going to explore the last in first out (LIFO) property of the stack.

Using only the following instructions:

    push
    pop

Swap values in rdi and rsi.

Example:

    If to start rdi = 2 and rsi = 5
    Then to end rdi = 5 and rsi = 2


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

