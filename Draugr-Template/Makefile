#Makefile

CCX64	=	x86_64-w64-mingw32-gcc
LDX64	= 	x86_64-w64-mingw32-ld

INCLUDE		= 	include/

CFLAGS	= -I./$(INCLUDE) -w -Os -s -m64 -masm=intel

all: prebuild core bof postbuild

prebuild:
	@ rm bin/*.o

core:
	@ nasm -f win64 src/asm/Utils.s -o bin/utils.o 
	@ $(CCX64) -c src/core/Spoof.c $(CFLAGS) -o bin/spoof.o
	@ $(CCX64) -c src/core/Syscalls.c $(CFLAGS) -o bin/syscalls.o


bof:
	@ $(CCX64) -c src/Main.c $(CFLAGS) -o bin/main.o
	@ $(LDX64) -r bin/*.o -o bin/draugr-template.o
	@ echo "[*] BOF Ready in bin/draugr-template.o !"

postbuild:
	@ rm bin/utils.o
	@ rm bin/main.o
	@ rm bin/spoof.o
	@ rm bin/syscalls.o


