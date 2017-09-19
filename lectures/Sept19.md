## Sept 19th Lecture
### Linking and Relocation
Def. **Relocation**: the process of adjusting addresses in macine lang code so it can be loaded at different memory 
addresses.

Def. An **object file** contains:

- machine lang code
- metadata describing what the labels used to be 

Assembly (a.s, b.s) -> *Assembler* -> Object Files (machine lang + metadata) (a.o, b.o) -> *Linker* -> Linked Machine Lang Program

Def. **Linking** is the process of combining object files into one program or library or object file

Example we want to export the labels from the following in our object file so we can Link
```Assembly
(b.s)
Define(a)
lis $1
Use(b)
jalr $1
jr $31
Define(b)
jr $31
```
Gets assembled to this which includes label info
```Machine
(b.o)
0 lis $1
4 16
8 jalr $1
12 jalr $31
16 jr $31 
meta: 
export label a = 0
       label b = 16
```

Another Example for Assembling Multiple Files with Dependent Labels
```Assembly
(a.s)
lis $1
Use(a)
jalr $1
jr $31
```
the label a is not defined so when we assemble we need to add metadata for the label a. 
So our object file would look something like
```Assembly
(a.o)
0 lis $1
4 ???? 0 
8 jalr $1
12 jr $31
meta: use label a at address 4
```
Now when we Link a.o and b.o we resolve the missing Labels by using the metadata. 
Note our assembled addresses in b.o would be wrong if we naively linked a.o and b.o so we must
**Relocate** the addresses in b.o (add a offset to each offset in this case by adding 16) 
**We also must update the exported labels with this offset**

The Linked version: 

```Assembly
0 lis $1
4 20  
8 jalr $1
12 jr $31
16 lis $1
20 32 
24 jalr $1
28 jalr $31
32 jr $31 
```

Linking should give the same output as concating the assembled code 
(as long as we don't have constants that rely on offsets)

### Variables
Def. A **variable** is an abstraction of a storage location that has a value
we translate variable into machine concepts

Def. the **extent** of a variable **instance** is the time interval
in which its value can be accessed

e.g. global variable -> entire execution of the program procedure

local variable -> one execution of procedure

e.g. 
```scala
def fact(x:Int): Int = if(x < 2) 1 else x * fact(x - 1) 
fact(3) = 3 * fact(2) = 3 * 2 * fact(1) = 3 * 2 * 1
```

Where is variable x? 
There is only one variable x but there are three instances at runtime

We can implement this with a stack.
We'll put the start of the stack at the end of memory. When we push we'll use lower addresses and when we pop we'll use higher.

Stack:

- designate storage register to store address of top of stack (**stack pointer**)
- push a word 
    - decrease stack pointer by 4
- pop a word 
    - increase stack pointer by 4
- by convention Reg(30) stores the stack pointer (sp)
- $30 is initialized to the end of memory






