# Level description
 
In this level, you will be working with registers. You will be asked to modify or read from registers.

In this level, you will work with registers! Please set the following:

- RDI = 0x1337

# Solution

1. Create the file:
```bash
nano solution.asm
```
2. Write the following in `solution.asm`:
```asm
global _start
_start:
	mov rdi,0x1337
	mov rax, 60
	syscall
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

This is the first flag from the Assembly Crash Course dojo, and is very simple. I recommend running `/challenge/run` as soon as you enter the challenge to see additional information.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` - the file will contain our code to capture the flag.

2. **Assembly code**:

- `global _start` -> declares the entry point for the linker.
- `_start:` -> line where execution begins.
- `mov rdi, 0x1337` -> sets register RDI as requested by the challenge.
- `mov rax, 60` -> 60 is the syscall number for 'exit' in 64 bits Linux.
- `syscall` -> executes the syscall above to exit the program.

3. **Assemble**: `nasm` convertes the human-readable assembly into an object file (`solution.o`) - machine code + info for the linker. Use `-f elf64` for 64-bits Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run** `/challnege/run /home/hacker/solution` submits the executable to the challenge environment, which will verify the registers and return the flag if requirements are met.

