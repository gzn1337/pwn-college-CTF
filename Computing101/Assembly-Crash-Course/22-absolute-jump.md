# Level description

We will now set some values in memory dynamically before each run. On each run, the values will change. This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

In this level, you will be working with control flow manipulation. This involves using instructions to both indirectly and directly control the special register rip, the instruction pointer. You will use instructions such as jmp, call, cmp, and their alternatives to implement the requested behavior.

Earlier, you learned how to manipulate data in a pseudo-control way, but x86 gives us actual instructions to manipulate control flow directly.

There are two major ways to manipulate control flow:

    Through a jump
    Through a call

In this level, you will work with jumps.

There are two types of jumps:

    Unconditional jumps
    Conditional jumps

Unconditional jumps always trigger and are not based on the results of earlier instructions.

As you know, memory locations can store data and instructions. Your code will be stored at 0x400042 (this will change each run).

For all jumps, there are three types:

    Relative jumps: jump + or - the next instruction.
    Absolute jumps: jump to a specific address.
    Indirect jumps: jump to the memory address specified in a register.

In x86, absolute jumps (jump to a specific address) are accomplished by first loading the target address into a general-purpose register (we'll call this placeholder reg), then doing jmp reg.

In this level, we will ask you to do an absolute jump. Perform the following: Jump to the absolute address 0x403000.

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	mov rax, 0x403000
	jmp rax
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

perform an absolute jump by directly setting the instruction pointer to the fixed address 0x403000.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.


2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov rax, 0x403000` → move the constant into rax.
- `jmp rax` → jump imediately to rax.
 

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.


4. **Link**: `ld solution.o -o solution` produces the final executable.


5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.


