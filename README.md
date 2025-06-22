# Assembly Lab – Print Text

## Objective

Print the following text using Assembly language and Linux syscalls:
I came,
I saw,
I conquered.
---
## How to Run This Code (Tested in JupyterHub Terminal)

### 1. Create the Assembly File

Open a terminal in JupyterLab and run:

```bash
nano first.asm

Paste the following code into the terminal:
section .data
    line1 db "I came,", 10      ; 10 = newline character
    line1_len equ $ - line1

    line2 db "I saw,", 10
    line2_len equ $ - line2

    line3 db "I conquered.", 10
    line3_len equ $ - line3

section .text
    global _start

_start:
    ; print line 1
    mov eax, 4          ; syscall number for write
    mov ebx, 1          ; file descriptor 1 = stdout
    mov ecx, line1      ; pointer to message
    mov edx, line1_len  ; message length
    int 0x80

    ; print line 2
    mov eax, 4
    mov ebx, 1
    mov ecx, line2
    mov edx, line2_len
    int 0x80

    ; print line 3
    mov eax, 4
    mov ebx, 1
    mov ecx, line3
    mov edx, line3_len
    int 0x80

    ; exit
    mov eax, 1          ; syscall for exit
    xor ebx, ebx        ; status = 0
    int 0x80

Assemble and Link
Now run the following commands in the terminal:
nasm -f elf first.asm -o first.o
ld -m elf_i386 first.o -o first

Run the Program
./first

Expected Output:
I came,
I saw,
I conquered.
