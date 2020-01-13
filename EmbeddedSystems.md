# EC308 Embedded Systems

## Assignment 1
* Students need to submit a bare-metal C program to blink an LED on and off continuously
  * On-Time = 1s
  * Off-Time = 1s
* Students have to program this on a baremetal AVR/Arduino platform.

### Hints
* Because we develop our software on an x86 or ARM computer, we need to perform a "cross-compilation" inorder to generate the binary for AVR architecture.
* avr-gcc installation.
  * Win-AVR on windows
  * sudo apt install gcc-avr binutils-avr
* [Code-Blocks IDE[https://codeblocks.org]] can be used to supervise Compile/Link etc.
  * sudo apt install codeblocks
  * You need to create a new project first and then a new c file within that project and enter the code.
* Compile and link can be initiated by clicking re-build button.
* avrdude installation.
  * avrdude is the software that we use to flash our program into the AVR chip.
  * sudo apt install avrdude
* Flash the program
  * avrdude -c usbasp -p m32 -U:flash:w:a.out

