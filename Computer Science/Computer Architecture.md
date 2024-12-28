# Computer Architecture Reference Sheet

## Processor Architecture

### Instruction Set Architecture (ISA)
1. **RISC vs CISC**
   ```
   RISC (Reduced Instruction Set Computing):
   - Simple instructions
   - Fixed instruction length
   - Load-store architecture
   - More registers
   
   CISC (Complex Instruction Set Computing):
   - Complex instructions
   - Variable instruction length
   - Memory-memory architecture
   - Fewer registers
   ```

2. **Common ISAs**
   ```
   x86/x86-64 (Intel/AMD):
   - CISC architecture
   - Backward compatibility
   - Complex encoding

   ARM:
   - RISC architecture
   - Power efficiency
   - Mobile/embedded focus

   RISC-V:
   - Open source
   - Modular design
   - Base + extensions
   ```

### Pipeline Stages
1. **Classic 5-Stage Pipeline**
   ```
   IF: Instruction Fetch
   ID: Instruction Decode
   EX: Execute
   MEM: Memory Access
   WB: Write Back
   ```

2. **Pipeline Hazards**
   ```
   Structural Hazards:
   - Resource conflicts
   - Hardware limitations

   Data Hazards:
   - RAW (Read After Write)
   - WAR (Write After Read)
   - WAW (Write After Write)

   Control Hazards:
   - Branch prediction
   - Pipeline flush
   ```

## Memory Hierarchy

### Cache Organization
1. **Cache Levels**
   ```
   L1 Cache:
   - Split I-cache/D-cache
   - Smallest, fastest
   - Typically 32-64KB

   L2 Cache:
   - Unified cache
   - Larger, slower
   - 256KB-1MB

   L3 Cache:
   - Shared cache
   - Largest, slowest
   - Several MB
   ```

2. **Cache Mapping**
   ```
   Direct Mapped:
   - One possible location
   - Simple, fast
   - More conflicts

   Set Associative:
   - N-way sets
   - Balance of complexity/performance
   - Common in modern CPUs

   Fully Associative:
   - Any location possible
   - Complex, expensive
   - Used for TLBs
   ```

### Memory Management
1. **Virtual Memory**
   ```
   Page Table:
   - Virtual to physical mapping
   - Page table entries (PTEs)
   - Multi-level structure

   TLB (Translation Lookaside Buffer):
   - Address translation cache
   - Hit rate > 99%
   - Fully associative
   ```

2. **Page Replacement**
   ```
   Algorithms:
   - LRU (Least Recently Used)
   - FIFO (First In First Out)
   - Clock algorithm
   - Random replacement
   ```

## System Bus and I/O

### Bus Architecture
1. **Bus Types**
   ```
   Address Bus:
   - Unidirectional
   - Memory addressing
   - Width determines addressable space

   Data Bus:
   - Bidirectional
   - Data transfer
   - Width determines transfer size

   Control Bus:
   - Various signals
   - Read/Write control
   - Timing signals
   ```

2. **Bus Protocols**
   ```
   Synchronous:
   - Clock-based timing
   - Simple design
   - Limited speed

   Asynchronous:
   - Handshaking protocol
   - More complex
   - Better performance
   ```

### I/O Systems
1. **I/O Methods**
   ```
   Programmed I/O:
   - CPU polling
   - Simple but inefficient
   - High CPU overhead

   Interrupt-Driven I/O:
   - CPU interrupts
   - Better CPU utilization
   - Interrupt overhead

   DMA (Direct Memory Access):
   - Independent transfers
   - Minimal CPU involvement
   - High performance
   ```

2. **I/O Interfaces**
   ```
   Serial:
   - USB
   - SATA
   - PCIe

   Parallel:
   - Legacy interfaces
   - Higher bandwidth
   - Limited distance
   ```

## Parallel Processing

### Parallelism Types
1. **Instruction-Level Parallelism (ILP)**
   ```
   Pipelining:
   - Overlapped execution
   - Multiple stages
   - Hazard handling

   Superscalar:
   - Multiple instructions per cycle
   - Out-of-order execution
   - Register renaming
   ```

2. **Thread-Level Parallelism (TLP)**
   ```
   Hardware Threads:
   - SMT (Simultaneous Multithreading)
   - Multiple thread contexts
   - Shared resources

   Multiple Cores:
   - Independent execution units
   - Shared cache
   - Inter-core communication
   ```

### Multiprocessor Systems
1. **SMP (Symmetric Multiprocessing)**
   ```
   Characteristics:
   - Shared memory
   - Uniform access time
   - Common bus/interconnect
   - Cache coherence
   ```

2. **NUMA (Non-Uniform Memory Access)**
   ```
   Characteristics:
   - Distributed memory
   - Variable access time
   - Local/remote memory
   - Scalability advantage
   ```

## Processor Performance

### Performance Metrics
1. **Basic Metrics**
   ```
   CPI (Cycles Per Instruction):
   - Base CPI
   - Pipeline stalls
   - Memory stalls

   IPC (Instructions Per Cycle):
   - 1/CPI
   - Superscalar factor
   - Pipeline efficiency
   ```

2. **Advanced Metrics**
   ```
   MIPS (Million Instructions Per Second):
   - Clock frequency
   - IPC
   - Instruction mix

   FLOPS (Floating Point Operations Per Second):
   - Floating point performance
   - Vector/SIMD capabilities
   - Precision levels
   ```

### Performance Optimization
1. **Hardware Techniques**
   ```
   Branch Prediction:
   - Static prediction
   - Dynamic prediction
   - Branch target buffer

   Speculative Execution:
   - Instruction prefetch
   - Data prefetch
   - Result prediction
   ```

2. **Memory Optimization**
   ```
   Cache Optimization:
   - Size/associativity
   - Replacement policy
   - Write policy

   Memory Hierarchy:
   - Cache levels
   - Prefetching
   - Bandwidth matching
   ```

## Security Features

### Hardware Security
1. **Memory Protection**
   ```
   Page Protection:
   - Read/Write/Execute bits
   - Privilege levels
   - Memory isolation

   ASLR (Address Space Layout Randomization):
   - Random base addresses
   - Stack/heap spacing
   - Library positioning
   ```

2. **Secure Execution**
   ```
   Trusted Execution Environment:
   - Secure enclave
   - Encrypted memory
   - Secure boot

   Hardware Encryption:
   - AES instructions
   - Random number generation
   - Key storage
   ```

### Virtualization Support
1. **Hardware Virtualization**
   ```
   CPU Features:
   - Virtual machine extensions
   - Nested paging
   - I/O virtualization

   Memory Features:
   - Extended page tables
   - IOMMU support
   - TLB tags
   ```

2. **Security Features**
   ```
   VM Isolation:
   - Hardware boundaries
   - Resource partitioning
   - Memory protection

   Secure Boot:
   - TPM support
   - Chain of trust
   - Key verification
   ```

## Power Management

### Power States
1. **CPU Power States**
   ```
   C-States (Idle):
   - C0: Operating
   - C1: Halt
   - C2: Stop Clock
   - C3+: Deep Sleep

   P-States (Performance):
   - Dynamic frequency
   - Voltage scaling
   - Power/performance trade-off
   ```

2. **System Power States**
   ```
   S-States:
   - S0: Working
   - S1: Sleep
   - S3: Suspend to RAM
   - S4: Suspend to Disk
   - S5: Soft Off
   ```

### Power Optimization
1. **Dynamic Management**
   ```
   DVFS (Dynamic Voltage and Frequency Scaling):
   - Workload adaptation
   - Temperature control
   - Battery life extension

   Power Gating:
   - Unit shutdown
   - Leakage reduction
   - Wake-up latency
   ```

2. **Thermal Management**
   ```
   Temperature Monitoring:
   - Thermal sensors
   - Critical thresholds
   - Throttling control

   Cooling Systems:
   - Passive cooling
   - Active cooling
   - Thermal design power
   ```
