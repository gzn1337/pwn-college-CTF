# Level description

We will now set some values in memory dynamically before each run. On each run, the values will change. This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

In this level, you will be working with memory. This will require you to read or write to things stored linearly in memory. If you are confused, go look at the linear addressing module in 'ike. You may also be asked to dereference things, possibly multiple times, to things we dynamically put in memory for your use.

Please perform the following:

    Place the value stored at 0x404000 into rax.
    Increment the value stored at the address 0x404000 by 0x1337.

Make sure the value in rax is the original value stored at 0x404000 and make sure that [0x404000] now has the incremented value.

# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	mov rax, [0x404000]
	add qword [0x404000], 0x1337
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


## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.


2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov rax, [0x404000]` →  store into rax, what is inside the 0x404000 address.
- `add qword [0x404000], 0x1337` → increment the value stored at 0x404000 by 0x1337.


3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.


4. **Link**: `ld solution.o -o solution` produces the final executable.


5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.

