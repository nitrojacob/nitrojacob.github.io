# EC308 Embedded Systems

## Assignment 1
* Objective: To make students familiar and comfortable with baremetal Embedded System Programming, the gnu compile toolchain and the cross-compile process flow. Also to familiarise students to embedded-C programming.
* Students need to submit a bare-metal C program to blink an LED on and off continuously
  * On-duration = 1s
  * Off-duration = 1s
* Students have to program this on a baremetal AVR platform. Students can save time by using the Arduino hardware if they wish to do so. But are not allowed to use arduino IDE or sketch. They are expected to write the C program, figure out the platform clock frequency, and division factor individually; and the compile/link/flash flows as group learning.
* Submission Date: 31/01/2020
* Grouping: Individual Submission
* Mode of submission: Will be published later.

### Hints
#### Tools
* Because we develop our software on an x86 or ARM(Raspberry Pi) computer, we need to perform a "cross-compilation" inorder to generate the binary for AVR architecture.
* Cross-compiler: avr-gcc installation.
  * [Win-AVR](http://winavr.sourceforge.net) on Windows
  * `sudo apt install gcc-avr binutils-avr` on Linux
* IDE(optional): [Code-Blocks IDE](https://codeblocks.org) can be used to supervise Compile/Link etc.
  * `sudo apt install codeblocks`
* avrdude installation.
  * avrdude is the software that we use to flash our program into the AVR chip.
  * `sudo apt install avrdude`

#### Procedure
* Create a new file
  * If using code-blocks IDE, you need to create a new project first and then a new c file within that project and enter the code.
  * Otherwise create a new file `main.c` and type in the program.
* Compile and link
  * can be initiated by clicking re-build button in code-blocks.
  * `avr-gcc main.c` does both compile and link.
* Flash the program
  * `avrdude -c usbasp -p m32 -U:flash:w:a.out`

