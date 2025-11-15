# Level description

In this level, you will be working with registers. You will be asked to modify or read from registers.

We will set some values in memory dynamically before each run. On each run, the values will change. This means you will need to perform some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result, which is usually rax.

This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result, which is typically in rax.

Another cool concept in x86 is the ability to independently access the lower register bytes.

Each register in x86_64 is 64 bits in size, and in the previous levels, we have accessed the full register using rax, rdi, or rsi.

We can also access the lower bytes of each register using different register names.

For example, the lower 32 bits of rax can be accessed using eax, the lower 16 bits using ax, and the lower 8 bits using al.

MSB                                    LSB
+----------------------------------------+
|                   rax                  |
+--------------------+-------------------+
                     |        eax        |
                     +---------+---------+
                               |   ax    |
                               +----+----+
                               | ah | al |
                               +----+----+

Lower register bytes access is applicable to almost all registers.

Using only one move instruction, please set the upper 8 bits of the ax register to 0x42.

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	mov ah, 0x42
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

Following the table in the level description, we can see the lower bits of **rax** register, and the one who we wanted to change was upper 8 bits **ah**.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.


2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov ah, 0x42` → put 0x42 in rax 8 bits upper register which is "**ah**". 


3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.


4. **Link**: `ld solution.o -o solution` produces the final executable.


5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

