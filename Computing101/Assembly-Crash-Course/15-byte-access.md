# Level description

We will now set some values in memory dynamically before each run. On each run, the values will change. This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

In this level, you will be working with memory. This will require you to read or write to things stored linearly in memory. If you are confused, go look at the linear addressing module in 'ike. You may also be asked to dereference things, possibly multiple times, to things we dynamically put in memory for your use.

Recall that registers in x86_64 are 64 bits wide, meaning they can store 64 bits. Similarly, each memory location can be treated as a 64-bit value. We refer to something that is 64 bits (8 bytes) as a quad word.

Here is the breakdown of the names of memory sizes:

    Quad Word = 8 Bytes = 64 bits
    Double Word = 4 bytes = 32 bits
    Word = 2 bytes = 16 bits
    Byte = 1 byte = 8 bits

In x86_64, you can access each of these sizes when dereferencing an address, just like using bigger or smaller register accesses:

    mov al, [address] <=> moves the least significant byte from address to rax
    mov ax, [address] <=> moves the least significant word from address to rax
    mov eax, [address] <=> moves the least significant double word from address to rax
    mov rax, [address] <=> moves the full quad word from address to rax

Remember that moving into al does not fully clear the upper bytes.

Please perform the following: Set rax to the byte at 0x404000.

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	mov al, [0x404000]
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

storing address content in rax lower 8 bits register.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov al, [0x404000]` →  store into al (rax lower 8 bits), what is inside the 0x404000 address.
3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.
