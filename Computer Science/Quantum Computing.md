# Quantum Computing Reference Sheet

## Quantum Mechanics Fundamentals

### Quantum Bits (Qubits)
1. **State Representation**
   ```
   |ψ⟩ = α|0⟩ + β|1⟩
   where |α|² + |β|² = 1
   ```

2. **Bloch Sphere**
   ```
   |ψ⟩ = cos(θ/2)|0⟩ + e^(iφ)sin(θ/2)|1⟩
   where:
   θ = polar angle
   φ = azimuthal angle
   ```

### Quantum Superposition
1. **Properties**
   ```
   - Linear combination of states
   - Simultaneous existence in multiple states
   - Collapses upon measurement
   ```

2. **Multiple Qubits**
   ```
   |ψ⟩ = α|00⟩ + β|01⟩ + γ|10⟩ + δ|11⟩
   where |α|² + |β|² + |γ|² + |δ|² = 1
   ```

### Quantum Entanglement
1. **Bell States**
   ```
   |Φ⁺⟩ = (|00⟩ + |11⟩)/√2
   |Φ⁻⟩ = (|00⟩ - |11⟩)/√2
   |Ψ⁺⟩ = (|01⟩ + |10⟩)/√2
   |Ψ⁻⟩ = (|01⟩ - |10⟩)/√2
   ```

2. **Properties**
   ```
   - Non-local correlations
   - Einstein-Podolsky-Rosen (EPR) paradox
   - Bell's inequality
   ```

## Quantum Gates and Circuits

### Single-Qubit Gates
1. **Pauli Gates**
   ```
   X (NOT) = [0 1]
             [1 0]

   Y = [0 -i]
       [i  0]

   Z = [1  0]
       [0 -1]
   ```

2. **Hadamard Gate**
   ```
   H = 1/√2 [1  1]
             [1 -1]
   ```

3. **Phase Gates**
   ```
   S = [1 0]
       [0 i]

   T = [1 0]
       [0 e^(iπ/4)]
   ```

### Multi-Qubit Gates
1. **CNOT (Controlled-NOT)**
   ```
   CNOT = [1 0 0 0]
          [0 1 0 0]
          [0 0 0 1]
          [0 0 1 0]
   ```

2. **SWAP**
   ```
   SWAP = [1 0 0 0]
          [0 0 1 0]
          [0 1 0 0]
          [0 0 0 1]
   ```

3. **Toffoli (CCNOT)**
   ```
   Three-qubit controlled-NOT gate
   Control qubits: 2
   Target qubit: 1
   ```

## Quantum Algorithms

### Deutsch-Jozsa Algorithm
1. **Problem**
   ```
   Determine if function f(x) is constant or balanced
   Classical: O(2^n-1 + 1) evaluations
   Quantum: O(1) evaluations
   ```

2. **Circuit**
   ```
   |0⟩ --[H]--[Uf]--[H]--
   |1⟩ --[H]--[Uf]--[H]--
   ```

### Grover's Algorithm
1. **Search Problem**
   ```
   Find marked item in unstructured database
   Classical: O(N) operations
   Quantum: O(√N) operations
   ```

2. **Oracle Operator**
   ```
   Oω|x⟩ = (-1)^f(x)|x⟩
   where f(x) = 1 for marked item
   ```

3. **Diffusion Operator**
   ```
   D = 2|ψ⟩⟨ψ| - I
   where |ψ⟩ is uniform superposition
   ```

### Shor's Algorithm
1. **Factorization**
   ```
   Find prime factors of N
   Classical: exp(O(log N)^1/3)
   Quantum: O(log N)^3
   ```

2. **Components**
   ```
   - Quantum Fourier Transform
   - Period finding
   - Classical post-processing
   ```

## Quantum Error Correction

### Error Types
1. **Bit Flip**
   ```
   |0⟩ → |1⟩
   |1⟩ → |0⟩
   ```

2. **Phase Flip**
   ```
   |0⟩ → |0⟩
   |1⟩ → -|1⟩
   ```

3. **Combined**
   ```
   Bit and phase errors
   Decoherence
   ```

### Error Correction Codes
1. **Three-Qubit Code**
   ```
   |0⟩ → |000⟩
   |1⟩ → |111⟩
   ```

2. **Shor Code**
   ```
   Nine-qubit code
   Protects against arbitrary errors
   ```

3. **Surface Codes**
   ```
   Topological quantum error correction
   High threshold
   ```

## Quantum Hardware

### Physical Implementations
1. **Superconducting Qubits**
   ```
   - Josephson junctions
   - Transmon qubits
   - Flux qubits
   ```

2. **Trapped Ions**
   ```
   - Electronic states
   - Laser cooling
   - Gate operations
   ```

3. **Photonic Qubits**
   ```
   - Linear optics
   - Single photons
   - Quantum interference
   ```

### Quantum Control
1. **Initialization**
   ```
   - Ground state preparation
   - Reset protocols
   - Verification
   ```

2. **Manipulation**
   ```
   - Microwave pulses
   - Laser control
   - Dynamic decoupling
   ```

## Quantum Programming

### Quantum Assembly Language
1. **QASM**
   ```qasm
   OPENQASM 2.0;
   include "qelib1.inc";
   
   qreg q[2];
   creg c[2];
   
   h q[0];
   cx q[0],q[1];
   measure q -> c;
   ```

2. **Pulse Programming**
   ```
   - Microwave sequences
   - Timing control
   - Calibration
   ```

### High-Level Languages
1. **Qiskit (IBM)**
   ```python
   from qiskit import *
   
   circuit = QuantumCircuit(2, 2)
   circuit.h(0)
   circuit.cx(0, 1)
   circuit.measure_all()
   ```

2. **Cirq (Google)**
   ```python
   import cirq
   
   qubits = [cirq.LineQubit(i) for i in range(2)]
   circuit = cirq.Circuit(
       cirq.H(qubits[0]),
       cirq.CNOT(qubits[0], qubits[1])
   )
   ```

## Quantum Applications

### Quantum Cryptography
1. **BB84 Protocol**
   ```
   - Quantum key distribution
   - No-cloning theorem
   - Basis reconciliation
   ```

2. **E91 Protocol**
   ```
   - Entanglement-based
   - Bell's inequality
   - Security proof
   ```

### Quantum Simulation
1. **Molecular Systems**
   ```
   - Electronic structure
   - Chemical reactions
   - Energy landscapes
   ```

2. **Material Science**
   ```
   - Phase transitions
   - Many-body systems
   - Quantum magnetism
   ```

## Performance Metrics

### Coherence Times
1. **T1 Time**
   ```
   Energy relaxation time
   Amplitude damping
   ```

2. **T2 Time**
   ```
   Phase coherence time
   Dephasing time
   ```

### Gate Fidelity
1. **Single-Qubit Gates**
   ```
   - Average gate fidelity
   - Process tomography
   - Randomized benchmarking
   ```

2. **Two-Qubit Gates**
   ```
   - CNOT fidelity
   - Cross-talk
   - Gate time
   ```

## Best Practices

### Circuit Optimization
1. **Gate Reduction**
   ```
   - Circuit decomposition
   - Gate cancellation
   - Template matching
   ```

2. **Layout Optimization**
   ```
   - Qubit mapping
   - Routing
   - Swap reduction
   ```

### Error Mitigation
1. **Measurement Error**
   ```
   - Readout calibration
   - Error matrices
   - Post-selection
   ```

2. **Gate Error**
   ```
   - Dynamical decoupling
   - Composite pulses
   - Virtual Z-gates
   ```
