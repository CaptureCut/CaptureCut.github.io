# Research Note #002  
## Exploring LLVM 21 Toolchain on Kali (2026)

### Overview
Kali Linux (2026) ships with a full LLVM 21 toolchain, including compilers,
linkers, IR tooling, JIT infrastructure, sanitizers, binary utilities,
profiling tools, and GPU/offload components.  
This makes the system suitable for low-level research, exploit development,
binary analysis, IR-level fuzzing, and compiler prototyping.

### 1. Clang Family
- clang
- clang++
- clang-21
- clang-check
- clang-query
- clang-refactor
- clang-scan-deps
- clang-apply-replacements
- clang-reorder-fields
- clang-move
- clang-doc
- clang-cl
- clang-cpp

### 2. Core LLVM Tools
- llc — IR → machine code
- lli — IR interpreter / JIT
- opt — IR optimization passes
- llvm-link — link multiple IR modules
- llvm-as / llvm-dis — IR assembler/disassembler

### 3. Binary Analysis
- llvm-objdump
- llvm-readelf
- llvm-readobj
- llvm-nm
- llvm-strings
- llvm-strip
- llvm-objcopy

### 4. Debugging & Symbolization
- llvm-symbolizer
- llvm-dwarfdump
- dsymutil
- llvm-debuginfo-analyzer

### 5. Profiling & Coverage
- llvm-profdata
- llvm-cov
- llvm-xray
- llvm-exegesis

### 6. Sanitizers
- asan_symbolize
- sancov
- sanstats

### 7. Build Analysis
- scan-build
- analyze-build
- intercept-build

### 8. GPU & Offloading
- clang-nvlink-wrapper
- nvptx-arch
- offload-arch
- clang-sycl-linker

### Observation
The presence of LLVM 21, Clang 21, and llvmlite 0.47.0 transforms Kali into
a fully capable engineering environment.  
This toolchain is directly relevant for:
- exploit-dev-auto
- JSC fuzzer research
- IR-level instrumentation
- JIT fuzzing prototypes
- CUDA/offload experiments
- binary analysis workflows

### Conclusion
Research Note #002 documents the discovery that Kali is not a lightweight
terminal environment but a complete low-level engineering platform.
