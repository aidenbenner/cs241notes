## Lecture 2 
### Sept 12
**Midterm Oct. 25 7pm - 8:50pm **


Encoding integers with 32 bits
- unsigned 0 to $2**32 - 1$
- signed $2**31$ to $2 ** 31 - 1$

**2's compliment**
Instead of regular binary numbers $$2**n * a_n, 2 ** n - 1, a_{n-1} ... 2 ** 0 n_{0}$$
Flip the sign of the highest power of 2 like: $$-2**n * a_n, 2 ** n - 1, a_{n-1} ... 2 ** 0 n_{0}$$

Benefits of 2's compliment
- each number has a unique bit representation
- can add to positive numbers regularly

- Hardware implements arithmetic mod $2 ** 32$
- Theorem: if $x \equiv x^` mod n$ $y \equiv y^`mod n$ then $x + y \equiv x^` + y^` mod n$
- same to add, subtract, multiply
- Need separate hardware for division

- Memory, 32 bits with $2 ** 22$ addresses
- CPU 34 registers with 32 bits per register
- Next to the CPU is the Control Unit
    - Circuit that changes the bits based 
    - implements a function 'Step'
        - a function from State_1 -> State_2 where States are the set of all bit strings

- A stored program computer
    - Includes a program as part of the input
    - Rather than hardcoding operations, use a piece of the memory to encode the program
    - So the hardware step function must be general to read these instructions

Registers and Memory Locations
- PC (Program Counter)
- **Note memory addresses differ by increments of 4**
- 

```scala
Step(state) = {
  // store instruction
  instr = state.mem[state.reg[PC]]
  state2 = state.setReg(PC, state.reg[PC] + 4)
  // execute instruction returns new state
  instr match {
    ...
  }
}

```


- different instructions for signed/unsigned inputs
- MIPS instruction sheet https://www.student.cs.uwaterloo.ca/~cs241e/current/mipsref.pdf
- magic value has to be written to PC to make marmoset stop running your code. Stored in reg 31? 



  

    






