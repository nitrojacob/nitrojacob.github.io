# EC308 Embedded Systems

[Lecture Slides](https://drive.google.com/open?id=1TX-RVMgG9Bpw5-rACOstmsd619kH-7J6)

[Video Lectures](https://drive.google.com/open?id=15i0zo1Qv8bDarNqqmRaYvfMqYPSKEnTW)

Quizes
Quizes shall be used to record attendance for each lecture. You need to score >=50 to secure attendance for the lecture.
* Module 4
  * [Lecture 1](https://forms.gle/3fddU6SCr7fiDDBf9)

## General
You can check the expectations of jobs in Embedded Systems at
  * [Job Listings at Naukri](https://www.naukri.com/vlsi-jobs?xt=catsrch&qf[]=24.05)
  * [Job Listings at Linkedin](https://www.linkedin.com/jobs/search?keywords=Embedded%20Systems&location=Karnataka%2C%20India&trk=guest_job_search_jobs-search-bar_search-submit&redirect=false&position=2&pageNum=0&f_E=2&currentJobId=1636246267)

For all assignments as part of this course, students have to program them on a baremetal AVR platform. Students can save time by using the Arduino hardware if they wish to do so. But are not allowed to use arduino IDE or sketch. They are expected to write the baremetal C program.

## Assignment 1
* Objective: To make students familiar and comfortable with baremetal Embedded System Programming, the gnu compile toolchain and the cross-compile process flow. Also to familiarise students to embedded-C programming.
* Students need to submit a bare-metal C program to blink an LED on and off continuously
  * On-duration = 1s
  * Off-duration = 1s
* Students are expected to write the C program, figure out the platform clock frequency, and division factor individually; and the compile/link/flash flows as group learning.
* Submission Date: 31/01/2020
* Grouping: Individual Submission
* Mode of submission: E-mail jacob(at)gecidukki.ac.in with subject line as `[EC308][Assignment 1]<roll#> <name>`
* Module Coverage: Module 1

### Hints
#### Tools
* Because we develop our software on an x86 or ARM(Raspberry Pi) computer, we need to perform a "cross-compilation" inorder to generate the binary for AVR architecture.
* Cross-compiler: avr-gcc installation.
  * [Win-AVR](http://winavr.sourceforge.net) on Windows. [Setup for windows](http://ladyada.net/learn/avr/setup-win.html)
  * `sudo apt install gcc-avr binutils-avr avr-libc` on Linux
* IDE(optional): [Code-Blocks IDE](https://codeblocks.org) can be used to supervise Compile/Link etc.
  * `sudo apt install codeblocks`
* avrdude installation.
  * avrdude is the software that we use to flash our program into the AVR chip.
  * `sudo apt install avrdude`
* [usbasp hardware](https://www.amazon.in/VEEROBOT-PROGRAMMER-USBasp-USBISP-MICROCONTROLLERS/dp/B00WFD21AW)
  * To connect your PC's USB to ICSP header of atmega; you need to use this protocol convertor.

#### Procedure
* Create a new file
  * If using code-blocks IDE, you need to create a new project first and then a new c file within that project and enter the code.
  * Otherwise create a new file `main.c` and type in the program.
* Compile and link
  * can be initiated by clicking re-build button in code-blocks.
  * `avr-gcc -mmcu=atmega328 main.c` does both compile and link.
* Flash the program
  * `avrdude -c usbasp -p m328p -U:flash:w:a.out` for bare chip without bootloader
  * `avrdude -c arduino -P /dev/ttyACM0 -p m328p -U:flash:w:a.out` for arduino boards with bootloader for serial download

#### Difference between arduino and atmega
* Arduino is a hardware platform (board with lots of standard 'hats') that is based on atmega
  * In-addition it provides a software ecosystem including IDE, bootloader and drivers.
  * The provided bootloader allows for program download over UART interface without using usbAsp or other external hardwares.
  * Fresh atmega without the bootloader only supports program download via ICSP.
  * The arduino bootloader is placed at high address of flash memory map. With or without the bootloader, the application entry point is 0x0. Hence same binary can be booted on all configurations of bootloader/application partition.

## Assignment 2
* Objective: To learn how to use behaviour and register descriptions in Programmers Reference Manual/datasheet to create a device driver. Learn about embedded C specifics of handling interrupts.
* Students need to submit a bare-metal C program to loopback UART. ie. it will send a message received on UART RxD port to TxD port; preferably after case inversion (Small letter -> capital and vice versa)
* Submission Date: 31/03/2020
* Grouping: Individual Submission
* Mode of submission: E-mail jacob(at)gecidukki.ac.in with subject line as `[EC308][Assignment 2]<roll#> <name>`
* Module Coverage: Module 2, 3

### Hints
* A driver is a set of functions implemented in one or two .c/.h files. Access to device registers are to be done only throuh corresponding driver.
* In case of uart, the driver should atleast provide following functions
  * `uart_init()` function to configure during init.
  * `uart_read()` function to read a character from uart.
  * `uart_write()` function to write a character to uart.
* In `main()` loop, you can call the above driver functions, along with code to modify the stream.
* Once basic functionality is demoed, considerations of what will happen if a UART Rx interrupt comes before execution of `uart_read()` etc, needs to be built.

## Assignment 3
* Objective: To learn how to setup and use RTOS for embedded systems.
* Students need to build freeRTOS port for AVR. Create and run two parallel tasks - 1. to blink an LED(from Assignment 1) and 2. to do uart loopback(from Assignment 2)
* Figure out the porting of freeRTOS to AVR as group activity. Task creation & using other RTOS calls etc as individual activity.
* Submission Date: 30/04/2020
* Grouping: Individual Submission
* Mode of submission: E-mail jacob(at)gecidukki.ac.in with subject line as `[EC308][Assignment 3]<roll#> <name>`
* Module Coverage: Module 5, 6

### Hints
* A sample port of freeRTOS for AVR is provided at https://github.com/nitrojacob/embedded-examples/tree/master/freeRTOS/AVR/blinky. Refer it in case you get stuck.
  * A slightly modified version of FreeRTOS-Kernel is required to build properly for AVR under avr-gcc compiler. https://github.com/nitrojacob/FreeRTOS-Kernel
  * The example was tested on the AVR simulator - simulavr and might have surprises with real chips. Its a bit hard to setup and use simulavr. But a guide for same is available at https://nitrojacob.wordpress.com/2020/03/30/simulavr-with-codeblocks/

