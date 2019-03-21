CROSS-COMPILER = arm-none-eabi-
QEMU = ./gnu-mcu-eclipse-qemu/bin/qemu-system-gnuarmeclipse

all: blink.bin

blink.bin: main.c blink.c vector_table.s
	$(CROSS-COMPILER)gcc -Wall -std=c11 -mcpu=cortex-m4 -mthumb -nostartfiles -T stm32f4.ld main.c blink.c vector_table.s -o blink.elf
	$(CROSS-COMPILER)objcopy -O binary blink.elf blink.bin

flash:
	st-flash --reset write blink.bin 0x8000000

qemu:
  $(QEMU) -M STM32F4-Discovery -nographic -gdb tcp::1234 -S -kernel blink.bin

clean:
	rm -f *.o *.elf *.bin
