cmake_minimum_required(VERSION 3.10.2)

project(FreeRTOS C)

set(FREERTOS_ROOT /home/jacob/programs/FreeRTOS-Kernel)
set(CMAKE_SYSYEM_NAME Generic)
set(CMAKE_SYSTEM_PROCESSOR avr)
set(CMAKE_C_COMPILER avr-gcc)

add_compile_options("-mmcu=atmega32")

add_executable(freertos main.c ${FREERTOS_ROOT}/tasks.c ${FREERTOS_ROOT}/portable/GCC/ATMega323/port.c)
target_include_directories(freertos PRIVATE ${FREERTOS_ROOT}/include ../freertos ${FREERTOS_ROOT}/portable/GCC/ATMega323)
