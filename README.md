# HierCIM: A 16-Kb SRAM-Based Digital CIM Macro With Hierarchical Adder-Tree Accumulation for Edge CNN Inference

## 📄 Paper Reference
HierCIM: A 16-Kb SRAM-Based Digital CIM Macro With Hierarchical Adder-Tree Accumulation for Edge CNN Inference

# Publication Link
[IEEE Xplore Paper](https://ieeexplore.ieee.org/abstract/document/11551984)
---

## 📌 Overview
This project presents a **16-Kb SRAM-based Digital Compute-in-Memory (CIM) architecture** designed for **energy-efficient edge AI inference**.

Traditional von Neumann architectures suffer from excessive **data movement between memory and compute units**, which dominates power and latency. This work addresses that bottleneck by enabling **in-memory computation**, where multiply-accumulate (MAC) operations are performed directly inside SRAM.

The architecture is optimized for:
- **1-bit activations**
- **1–4 bit weights**
- Low-power, high-throughput CNN inference

---

## 🚀 Key Contributions
- Compute-enabled **NOR-based 6T+4T SRAM cell**
- **64-bank parallel CIM architecture**
- **Rearrangement network** for structured data flow
- **Sparsity-aware 4:3 compressor** for power reduction
- **38T PTL-based compact 4-bit adder**
- **Hierarchical adder-tree accumulation**
- **Counter-based Shift-and-Accumulate (SAC) engine**
- Full **ASIC design flow validation (65 nm CMOS)**

---

## 🧠 Motivation
Traditional Architecture:
Memory <-> Processor  --> High Energy + High Latency

Compute-in-Memory:
Memory + Compute      --> Minimal Data Transfer


✔ Reduces energy consumption  
✔ Improves throughput  
✔ Enables efficient edge AI  

---

## 🏗️ Architecture Overview

The proposed macro consists of:
- **64 CIM banks**
- Each bank: **64 × 4 SRAM array**

### Dataflow:
1. Input activations are broadcast to all banks  
2. Weights are stored in SRAM cells  
3. Bitwise multiplication occurs inside memory  
4. Outputs are rearranged and compressed  
5. Partial sums are accumulated via adder tree  
6. SAC engine produces final MAC output  

---

## ⚙️ Core Components

### 1. Compute-Enabled SRAM Cell
- Based on standard 6T SRAM with added NOR compute path
- Performs **in-memory bitwise multiplication**

**Key Idea:**
- Weight stored in SRAM
- Activation applied externally
- NOR logic produces multiplication equivalent

✔ Eliminates external multipliers  
✔ Maintains array regularity  

---

### 2. Rearrangement Network
- Aligns partial products column-wise before compression
  
✔ Reduces the number of cases from 16 to 5 for further compression. Hence leading to results with least approximation.
✔ Reduces routing complexity  
✔ Prepares data for efficient reduction  

---

### 3. Sparsity-Aware 4:3 Compressor
- Compresses 4 inputs → 3 outputs (C2, C1, S)
- Includes **zero-detection gating**

✔ Disables switching when inputs are zero  
✔ Reduces dynamic power consumption  

---

### 4. Compact 4-bit Adder (38T PTL Design)
- Low transistor count implementation
- Optimized for speed and area

✔ Reduced logic depth  
✔ Efficient accumulation  

---

### 5. Hierarchical Adder Tree
- Reduces 64 inputs in multiple stages
- Uses compressors + adders

✔ Shorter critical path  
✔ High parallelism  
✔ Improved throughput  

---

### 6. Shift-and-Accumulate (SAC) Engine

Performs multi-bit MAC using sequential accumulation using counter and MUX based approach for proper left shift synced with clock cycle.

#### Operation:
- Weight = 4-bit → processed over 4 cycles
- Each cycle:
  - Partial product generated
  - Shifted according to bit position
  - Accumulated in registered
  - Final output achieved.

## 🧮 CNN Mapping

- Network: **LeNet-5**
- Datasets:
  - MNIST
  - CIFAR-10

### Configuration:
- Activations: 1-bit  
- Weights: 4-bit  

### Mapping Strategy:
- Each convolution kernel → mapped to CIM banks  
- Parallel processing across banks  
- Fully connected layers → matrix-vector mapping  

---

## 📊 Performance Results

| Metric | Value |
|------|------|
| Technology | 65 nm CMOS |
| Macro Size | 16 Kb |
| Area | 4.5 mm² |
| Max Throughput | 8.19 TOPS @ 1.0 V |
| Energy Efficiency | 586 TOPS/W @ 0.9 V |
| Power | 6.99 mW |
| MNIST Accuracy | 98.1% |
| CIFAR-10 Accuracy | 72.3% |

---

## 🧩 Design Highlights

- Fully **digital architecture** (no ADC/DAC)
- High robustness against:
  - Noise
  - Process variations
- Scalable **banked structure**
- Optimized for **low-bit AI inference**

---

## 🏁 Conclusion
This work demonstrates a **practical and scalable SRAM-based CIM architecture** that achieves:

- High throughput  
- High energy efficiency  
- Robust digital operation  

The integration of **rearrangement, sparsity-aware compression, and hierarchical accumulation** enables efficient in-memory MAC operations suitable for edge AI applications.

---

## 🙌 Acknowledgement
Supported by **MeitY (Chips to Startup Program)** for EDA tools and funding.

