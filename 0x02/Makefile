CFLAGS=-O0 -g -Wall

nasm: lin32 lin64

x64: lin64

x32: lin32

lin32:
	nasm -f elf32 arithmetic32.asm -o arithmetic32.o
	gcc $(CFLAGS) -m32 generator.c -o generator
	gcc $(CFLAGS) -m32 arithmetic_asm.c arithmetic32.o -o arithmetic_asm32
	gcc $(CFLAGS) -m32 arithmetic_c.c -o arithmetic_c

lin64:
	nasm -f elf64 arithmetic64.asm -o arithmetic64.o
	gcc $(CFLAGS) -m64 generator.c -o generator
	gcc $(CFLAGS) -m64 arithmetic_asm.c arithmetic64.o -o arithmetic_asm64
	gcc $(CFLAGS) -m64 arithmetic_c.c -o arithmetic_c

mac64:
	nasm -f macho64 arithmetic64.asm -o arithmetic64.o
	gcc $(CFLAGS) -m64 arithmetic_asm.c arithmetic64.o -o arithmetic_asm64
	gcc $(CFLAGS) -m64 arithmetic_c.c -o arithmetic_c

mac32:
	nasm -f macho32 arithmetic32.asm -o arithmetic32.o
	gcc $(CFLAGS) -m32 arithmetic_asm.c arithmetic32.o -o arithmetic_asm32
	gcc $(CFLAGS) -m32 arithmetic_c.c -o arithmetic_c

lindump:
	objdump -M intel -d arithmetic_asm32 > objdump_asm32
	objdump -M intel -d arithmetic_asm64 > objdump_asm64
	objdump -M intel -d arithmetic_c > objdump_c

macdump:
	objdump -x86-asm-syntax=intel -D arithmetic_asm32 > objdump_asm32
	objdump -x86-asm-syntax=intel -D arithmetic_asm64 > objdump_asm64
	objdump --x86-asm-syntax=intel -D arithmetic_c > objdump_c

generator:
	gcc $(CFLAGS) generator.c -o generator

geninput: generator
	./generator 9999999 > input.txt

compare: geninput
	time ./arithmetic_asm32 < input.txt > output_asm32.txt
	time ./arithmetic_asm64 < input.txt > output_asm64.txt
	time ./arithmetic_c < input.txt > output_c.txt

clean:
	rm -rf *.o objdump_* input.txt output_* *.dSYM arithmetic_c arithmetic_asm32 arithmetic_asm64 generator
