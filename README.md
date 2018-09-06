# Firstly, you will be needed in NASM. Follow steps below to install:

Install homebrew by running following line in terminal. 
If you already have it - you can skip this step.
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now install nasm via homebrew:
```
brew install nasm
```

That's it. 

# Now lets do our first assembly.

Create file helloWorld.asm by running:
```
touch helloWorld.asm
```

Open it (```open -a textedit helloWorld.asm```), paste this lines and save:
```
global start

section .text

start:
    mov     rax, 0x2000004 ; write
    mov     rdi, 1 ; stdout
    mov     rsi, msg
    mov     rdx, msg.len
    syscall

    mov     rax, 0x2000001 ; exit
    mov     rdi, 0
    syscall


section .data

msg:    db      "Hello, world!", 10
.len:   equ     $ - msg
```

Run this commands to create Unix executable file:
```
nasm -f macho64 helloWorld.asm

ld -macosx_version_min 10.7.0 -lSystem -o hello helloWorld.o
```

You can start your hello to see the result. To start your executable file run:
```
./hello
```
