### Tools

```
sudo apt update
sudo apt install -y nasm gcc gdb readelf
```

Other tools are `file`, `objdump` and `hexdump` (aka `hd`).

### Template

Template for elf64 executable format.

```asm
BITS 64

; Elf file requires a _start symbol (the entry point) and a main symbol.

GLOBAL _start:

SECTION	.text

main:
    mov rax, 3
    mov rbx, 4
    add rax, rbx
    ret

_start:
    call main
    mov rdi, rax
    mov rax, 60
    syscall         ; For 64-bit linux.
                    ; See https://stackoverflow.com/a/19760081/1124350
```

### Compiling

```sh
nasm -g -f elf64 template.asm
ld template.o
```

`-g` flag to produce debugging information.

### Debugging with gdb

```sh
gdb template.out
(gdb) start
(gdb) layout regs
(gdb) si
```
