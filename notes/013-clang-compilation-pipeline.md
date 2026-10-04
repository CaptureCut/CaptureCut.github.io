Title: Clang-Compilation-Pipeline-and-Optimization

Date: 2026-10-02

Goal

Understand how Clang compiles C programs and observe how optimization changes LLVM IR and assembly output.

Environment

Kali Linux
Clang 21.1.8
LLVM 21

Source Code

Experiment 1:

int add(int a, int b) {
    return a + b;
}

int main() {
    return add(10, 20);
}

Compiler Inspection

Command:

clang -### ~/Desktop/test.c -o test

Observation

Clang revealed the internal compilation pipeline.

Pipeline:

C Source
↓
clang -cc1
↓
Object File (.o)
↓
Linker (ld)
↓
ELF Executable

Observed Components

clang -cc1
/usr/bin/ld
libc (-lc)
crt startup objects

Result

Confirmed that Clang is a compiler driver that invokes multiple tools during compilation.

Assembly Generation

Command:

clang -S ~/Desktop/test.c

Observation

Generated assembly file:

test.s

Assembly (O0)

Function add:

movl    %edi, -4(%rbp)
movl    %esi, -8(%rbp)
movl    -4(%rbp), %eax
addl    -8(%rbp), %eax

Function main:

movl    $10, %edi
movl    $20, %esi
callq   add

Result

Observed traditional function calling and stack frame setup.

Optimization Test

Command:

clang -O2 -S ~/Desktop/test.c -o opt.s

Observation

Function add:

leal    (%rdi,%rsi), %eax
retq

Function main:

movl    $30, %eax
retq

Result

The compiler removed the function call entirely and replaced it with a constant result.

Observed Optimizations

Constant Folding
Constant Propagation
Function Simplification

LLVM IR Generation

Command:

clang -O0 -S -emit-llvm ~/Desktop/test.c -o O0.ll

Observation

LLVM IR retained the original program structure.

Example:

%4 = call i32 @add(i32 noundef 10, i32 noundef 20)

Result

LLVM IR closely matched the source code.

Optimized LLVM IR

Command:

clang -O2 -S -emit-llvm ~/Desktop/test.c -o O2.ll

Observation

main became:

ret i32 30

The function call disappeared.

Result

Optimization occurred inside LLVM IR before assembly generation.

Additional Experiment

Source Code

int square(int x) {
    return x * x;
}

int main() {
    int n = 5;
    return square(n);
}

LLVM IR (O0)

call i32 @square(...)
mul nsw i32

LLVM IR (O2)

ret i32 25

Result

LLVM evaluated the function during compilation and replaced the execution path with a constant value.

Key Concepts

Clang Driver
Coordinates compilation stages.

clang -cc1
Internal compiler frontend.

LLVM IR
Intermediate Representation used for analysis and optimization.

Assembly
Human-readable CPU instructions.

Linker
Combines objects and libraries into a final executable.

Constant Folding
Compile-time evaluation of constant expressions.

Conclusion

Confirmed the complete compilation pipeline:

C
↓
Clang Frontend
↓
LLVM IR
↓
Optimization
↓
Assembly
↓
Object File
↓
Linker
↓
ELF

Observed that most code transformations and optimizations occur at the LLVM IR stage before final machine code generation.
