# Level description

In this level, you will be working with registers. You will be asked to modify or read from registers.

In this level, you will work with multiple registers. Please set the following:

- RAX = 0x1337
- R12 = 0xCAFED00D1337BEEF
- RSP = 0x31337

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:
    mov r12, 0xCAFED00D1337BEEF
    mov rsp, 0x31337
    mov rax, 0x1337
```

> Note: This code sets the required registers. Some challenge runners read registers without needing the process to exit; if your runner requires the program to exit, you'll need to adjust the code so the exit syscall doesn't overwrite the required register values at the time of checking.

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
- Flag received — output saved in `level-2.png`.

# Notes

Another simple challenge. I recommend running `/challenge/run` as soon as you enter the challenge to see additional information.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.  
- `_start:` → label where execution begins.  
- `mov r12, 0xCAFED00D1337BEEF` → sets R12 as requested.  
- `mov rsp, 0x31337` → sets RSP as requested.  
- `mov rax, 0x1337` → sets RAX as requested.  

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

6. **Flag**: Output captured in `level-2.png`.
