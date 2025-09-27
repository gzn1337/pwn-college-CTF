# Level description:

In this level, you will be working with registers. You will be asked to modify or read from registers.

In this level, you will work with multiple registers. Please set the following:

    rax = 0x1337
    r12 = 0xCAFED00D1337BEEF
    rsp = 0x31337

# Solution:

1 - :~ nano solution.asm
2 - :~ write in solution.asm =
global _start
_start:
        mov r12, 0XCAFED00D1337BEEF
	mov rsp, 0x31337
	mov rax, 0x1337

3 - :~ nasm -f elf64 solution.asm -o solution.o
4 - :~ ld solution.o -o solution
5 - :~ /challenge/run /home/hacker/solution
6 - :~ flag received, the output can be seen in level-2.png!


# Notes:

another simple challenge, i recommend to always execute /challenge/run as soon as you enter the challenge to view more information.

step by step explained >>

1 >> creating an assembly file with nano solution.asm which will contain our code to capture the flag.

2 >> the code!

3 >>

global _start -> declares the entry point for the linker.
_start: -> line where execution begins.
mov r12, 0XCAFED00D1337BEEF -> sets the register R12 to 0xCAFED00D1337BEEF as requested by the challenge.
mov rsp, 0x31337 -> sets the register RSP to 0x31337 as requested by the challenge.
mov rax, 0x1337	-> sets the register RAX to 0x1337 as requested by the challenge.
 
4 >> linking the object file with LD, ld combines object files and libraries into a executable by resolving symbols, arranging sections, and producing the binary.

5 >> running /challenge/run command with the path to our executable, now the challenge will override and verify if all the requisites are completed and return the flag if succeed.

6 >> flag received! :D
