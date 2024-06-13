# Twig Specification - rev1a

Twig is a stack-based emulator/interpreter. It is inspired by the CHIP-8 and Forth. Twig is meant to be a multiplatform way of 
writing software with minimal code. It provides a bare bones environment to do what ever you want with everything you would 
need. It can be implemented fairly easy and should be very performant.

# Display
The display has 6 modes that can be set. The display can be scaled with a command-line parameter for larger displays.

* 640x480 (4:3) - 0x1
* 800x600 (4:3) - 0x2
* 1024x768 (4:3) - 0x3
* 1280x720 (16:9) - 0x4
* 1600x900 (16:9) - 0x5
* 1920x1080 (16:9) - 0x6

# Input
Currently only keyboard is supported but mouse will be in the future specification versions. The key pressed is pushed to the top of the stack.

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
Opcodes can be 1 byte or 9 bytes long. 9 bytes instructions are when the instruction requires an operand.
```
IN = 64-bit integer

(hlt)    00    - Halt

(setv)   01    - Pop integer off the top of the stack and set the video mode to it.
(getv)   02    - Get the video mode and push it to top of the stack.

(getk)   10    - Get the key pressed and push it to top of the stack.
(getmc)  11    - Get the current mouse x and y coordinates and push them to top of the stack.
(getmp)  12    - Get the which mouse button has been pressed. If left button was pressed push 1,
                 if middle button was pressed push 2 and if right button was pressed push 3. 

// SOUND TODO //

(get)    30    - Pop integer off the top of the stack and get the data in memory from it.
(set)    31    - Pop 2 integers off the top of the stack (top, below) and set the memory at below to top.

(push)   40 IN - Push integer to top of the stack.
(pop)    41    - Pop integer off the top of the stack.
(rpush)  42 IN - Push integer to top of the return stack.
(rpop)   43    - Pop integer off the top of the return stack.
(ret)    44    - Pop integer off the top of the return stack and set PC to it.

(add)    50   - Pop the top 2 integers off the stack (top, below), do below + top, then push the result to the top.
(sub)    51   - Pop the top 2 integers off the stack (top, below), do below - top, then push the result to the top.
(mul)    52   - Pop the top 2 integers off the stack (top, below), do below * top, then push the result to the top.
(div)    53   - Pop the top 2 integers off the stack (top, below), do below / top, then push the result to the top.
(shr)    54   - Pop the top 2 integers off the stack (top, below), do below >> top, then push the result to the top.
(shl)    55   - Pop the top 2 integers off the stack (top, below), do below << top, then push the result to the top.
(and)    56   - Pop the top 2 integers off the stack (top, below), do below & top, then push the result to the top.
(or)     57   - Pop the top 2 integers off the stack (top, below), do below | top, then push the result to the top.
(xor)    58   - Pop the top 2 integers off the stack (top, below), do below ^ top, then push the result to the top.

(equ)    60   - Pop the top 2 integers off the stack (top, below), do below == top, then if true push 1 to the else push 0.
(neq)    61   - Pop the top 2 integers off the stack (top, below), do below != top, then if true push 1 to the else push 0.
(gt)     62   - Pop the top 2 integers off the stack (top, below), do below > top, then if true push 1 to the else push 0.
(lt)     63   - Pop the top 2 integers off the stack (top, below), do below < top, then if true push 1 to the else push 0.
(gte)    64   - Pop the top 2 integers off the stack (top, below), do below >= top, then if true push 1 to the else push 0.
(lte)    65   - Pop the top 2 integers off the stack (top, below), do below <= top, then if true push 1 to the else push 0.

// TODO : FINISH OPCODES

```
