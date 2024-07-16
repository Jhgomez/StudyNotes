# Compilers 2 Concepts

### RISC vs CISC
RISC stands for "Reduced Instruction Cycle", CISC is "Complex Instruction Cycle". 

Comparison from RISC point of view:

subjective(can be a downside or updside):
- RISC instructions are simple, perform only one operation, and a CPU can execute them in one cycle while CISC instructions are packed in a bunch of operations, meaning CISC instructions are complex but can perform multiple operations which reduces the amount of code needed to perform a task

upsides:
- Decoding instructions in RISC is simple, whereas, in CISC is complex. This means RISC executes faster
- RISC doesn't require external memory for calculations, on the other hand CISC does
- RISC has multiple registers sets present, while CISC has onlly a single registe set
- RISC processors power compsumption is lower, making them ideal for portable devices

downsides:
 
 - RISC requires more instructions to perform complex task than CISC. This is because CISC instructions are complex but can perfor 
 - RISC requires more memory(Increased memory usage) to store aditional instructions than CISC to perform complex tasks, this is because CISC instructions are complex but can execute complex task with less instructions
 

#### RISC Based Processors
More used in portable devices
- RISC-V
- ARM
- Raspberry Pi

#### CISC Based Processors
More used in desktop computers, servers
- X86, x64 and x86-64 processors from intel
- AMD