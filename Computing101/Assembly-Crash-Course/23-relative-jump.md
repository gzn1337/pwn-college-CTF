# Level description

We will now set some values in memory dynamically before each run. On each run, the values will change. This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

In this level, you will be working with control flow manipulation. This involves using instructions to both indirectly and directly control the special register rip, the instruction pointer. You will use instructions such as jmp, call, cmp, and their alternatives to implement the requested behavior.

Recall that for all jumps, there are three types:

    Relative jumps
    Absolute jumps
    Indirect jumps

In this level, we will ask you to do a relative jump. You will need to fill space in your code with something to make this relative jump possible. We suggest using the nop instruction. It's 1 byte long and very predictable.

In fact, the assembler that we're using has a handy .rept directive that you can use to repeat assembly instructions some number of times: GNU Assembler Manual

Useful instructions for this level:

    jmp (reg1 | addr | offset)
    nop

Hint: For the relative jump, look up how to use labels in x86.

Using the above knowledge, perform the following:

    Make the first instruction in your code a jmp.
    Make that jmp a relative jump to 0x51 bytes from the current position.
    At the code location where the relative jump will redirect control flow, set rax to 0x1.


# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	jmp destino
	times 0x51 nop
	destino:
	mov rax, 1
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

here we use a relative jump to skip 0x51 bytes and sets rax to 1 at the jump target, demonstrating control flow manipulation.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.


2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `jmp destino` → perform a relative jump to "destino", jumping all informations between here and the "destino:"
- `times 0x51 nop` → fills 0x51 bytes with nop instructions, which do nothing and just occupy space for the relative jump.
- `destino:` → label marking the jump target.
- `mov rax, 1` →sets the value 1 in the rax register.
 

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.


4. **Link**: `ld solution.o -o solution` produces the final executable.


5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.
