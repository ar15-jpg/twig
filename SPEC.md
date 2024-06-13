# Twig Specification rev1a

Twig is a stack-based emulator/interpreter. It is inspired by the CHIP-8 and Forth. Twig is meant to be a multiplatform way of 
writing software with minimal code. It provides a bare bones environment to do what ever you want with everything you would 
need. It can be implemented fairly easy and should be very performant.

# Display
The display has 6 modes that can be set. The display can be scaled with a command-line parameter for larger displays.

* 640x480 (4:3)
* 800x600 (4:3)
* 1024x768 (4:3)
* 1280x720 (16:9)
* 1600x900 (16:9)
* 1920x1080 (16:9)

# Input
Currently only keyboard is supported but mouse will be in the future specification versons

# Sound
TODO.

# Memory
This is how the memory is layed out:
```
############################################
# Display memory (36000 bytes for 600x400) #
############################################
#                                          #
#               Free memory                #
#                                          #
############################################
#              Program memory              #
############################################
```

# Stack
The stack is capped at 128 cells that are 64-bit integers. 128 cells is very excessive for this and if a program is using more than 
that 128 cells the code must be refactored. There is also a return stack, which has the same properties as the stack but the return
stack is only used for return to a previous location in the program.

# Registers
* PC - Program couter
* SP - Stack pointer
* RSP - Return stack pointer

# Opcodes
Opcodes can be 1 byte or 9 bytes long. 9 bytes instructions are when the instruction requires some sort of direct input that is not
taken off the stack.
```
IN = 64-bit integer

(hlt)   00    - Halt

(push)  01 IN - Push integer to top of the stack
(pop)   02    - Pop integer off the top of the stack
(rpush) 03 IN - Push integer to top of the return stack
(rpop)  04    - Pop integer off the top of the return stack
(ret)   05    - Pop integer off the top of the return stack and set PC to it.

(get)   10    - Pop integer off the top of the stack and get the data in memory from it.
(set)   11    - Pop 2 integers off the top of the stack (top, below) and set the memory at below to top
 

```
