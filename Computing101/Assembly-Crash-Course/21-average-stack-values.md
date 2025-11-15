# Level description

We will now set some values in memory dynamically before each run. On each run, the values will change. This means you will need to do some type of formulaic operation with registers. We will tell you which registers are set beforehand and where you should put the result. In most cases, it's rax.

In this level, you will be working with the stack, the memory region that dynamically expands and shrinks. You will be required to read and write to the stack, which may require you to use the pop and push instructions. You may also need to use the stack pointer register (rsp) to know where the stack is pointing.

In the previous levels, you used push and pop to store and load data from the stack. However, you can also access the stack directly using the stack pointer.

On x86, the stack pointer is stored in the special register, rsp. rsp always stores the memory address of the top of the stack, i.e., the memory address of the last value pushed.

Similar to the memory levels, we can use [rsp] to access the value at the memory address in rsp.

Without using pop, please calculate the average of 4 consecutive quad words stored on the stack. Push the average on the stack.

Hint:

    RSP+0x?? Quad Word A
    RSP+0x?? Quad Word B
    RSP+0x?? Quad Word C
    RSP Quad Word D


# Solution

1. Create the file:
```bash
nano solution.asm
```

2. Write the following in `solution.asm`:
```asm
global _start

_start:

	mov rax, [rsp]
	mov rcx, [rsp+8]
	mov rbx, [rsp+16]
	mov rdi, [rsp+24]

	add rax, rcx
	add rax, rbx
	add rax, rdi

	sar rax, 2

	push rax
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

this challenge demonstrates how to access consecutive values on the stack using [rsp+offset], perform arithmetic without popping, and push the result back safely.

## Steps explained

1. **Create the assembly file**: `nano solution.asm` — the file will contain our code to capture the flag.

2. **Assembly code**:
- `global _start` → declares the entry point for the linker.
- `_start:` → line where execution begins.
- `mov rax, [rsp]` → loads the value at the top of the stack into **rax**.
- `mov rcx, [rsp+8]` → loads the next value on the stack into **rcx**.
- `mov rbx, [rsp+16]` → loads the next consecutive stack value into **rbx**.
- `mov rdi, [rsp+24]` → loads the fourth consecutive stack value into **rdi**.
- `add rax, rcx` → adds **rcx** to **rax** (partial sum).
- `add rax, rbx` → adds **rbx** to **rax** (partial sum).
- `add rax, rdi` → adds **rdi** to **rax** (total sum).
- `sar rax, 2` → divides **rax** by 4 to compute average.
- `push rax` → pushes the computed average onto the top of the stack.
 

3. **Assemble**: `nasm` converts the human-readable assembly into an object file (`solution.o`) — machine code + info for the linker. Use `-f elf64` for 64-bit Linux.

4. **Link**: `ld solution.o -o solution` produces the final executable.

5. **Run**: `/challenge/run /home/hacker/solution` submits the executable to the challenge environment, which verifies the registers and returns the flag if requirements are met.
