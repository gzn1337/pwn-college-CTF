# Level description:
 
In this level, you will be working with registers. You will be asked to modify or read from registers.

In this level, you will work with registers! Please set the following:

	rdi = 0x1337


# Solution:

1 - :~ nano solution.asm
2 - :~ write in solution.asm =
global _start
_start:
	mov rdi,0x1337
	mov rax, 60
	syscall
3 - :~ nasm -f elf64 solution.asm -o solution.o
4 - :~ ld solution.o -o solution
5 - :~ /challenge/run /home/hacker/solution
6 - :~ flag received, the output can be seen in level-1.png
 
# Notes:

this is the first flag from the Assembly Crash Course dojo, and is very simple.

steps explained:

1 >> creating an assembly file with nano solution.asm which will contain our code to capture the flag.

2 >> the code!

global _start -> declares the entry point for the linker.
_start: -> line where execution begins.
mov rdi, 0x1337 -> sets register RDI to 0x1337 as requested by the challenge.
mov rax, 60 -> 60 is the syscall number for 'exit' in 64 bits Linux.
syscall -> executes the syscall above to exit the program.

3 >> assemble the code with NASM or GAS, i'm using NASM here, nasm converts the human readable assembly into an object file which your machine can read, with another words, this will change something like mov rdi, 0x1337 to bytes.
-f elf64 -> target format is 64 bits ELF(Executable and Linkable Format).
solution.o -> output object file. (object file: a file that is not a 100% executable, he contains machine code + informations to the linker(who gonna be used in next step).

4 >> linking the object file with LD, ld combines object files and libraries into a executable by resolving symbols, arranging sections, and producing the binary.

5 >> running /challenge/run command with the path to our executable, now the challenge will override and verify if all the requisites are completed and return the flag if succeed.

6 >> flag received! :)
