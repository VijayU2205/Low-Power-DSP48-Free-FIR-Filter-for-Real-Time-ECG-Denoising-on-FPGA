# Low-Power DSP48-Free FIR Filter for Real-Time ECG Denoising on FPGA

---

## Abstract

Electrocardiogram (ECG) signals are highly susceptible to various sources of noise such as power-line interference, muscle artifacts, and high-frequency disturbances, which can reduce the accuracy of cardiac diagnosis. This project presents a **low-power, DSP48-free FIR filter architecture** implemented on an **Artix-7 FPGA** for real-time ECG denoising.

Instead of using dedicated DSP48 multiplier blocks, the proposed design employs **symmetric coefficient folding**, **shift-and-add multiplication**, and **vertical pipelining** to reduce hardware complexity and dynamic power consumption while maintaining filtering performance. ECG samples generated in MATLAB are streamed to the FPGA, processed in real time, and transmitted to a Python-based visualization dashboard through UART communication.

The implemented architecture demonstrates efficient real-time ECG filtering with low resource utilization, making it suitable for wearable healthcare devices, portable biomedical instruments, and energy-efficient embedded systems.

---

## Keywords

FPGA, FIR Filter, ECG Denoising, Low-Power Design, DSP48-Free Architecture, Shift-and-Add Multiplication, Symmetric FIR Filter, UART Communication, Real-Time Signal Processing, Artix-7 FPGA

---

## Problem Statement

ECG signals acquired from patients are often contaminated by noise introduced from electrical interference, muscle activity, and motion artifacts. Conventional FPGA implementations of FIR filters typically depend on DSP48 multiplier blocks, which increase hardware utilization and dynamic power consumption.

For wearable and battery-operated healthcare systems, there is a growing need for a hardware-efficient ECG filtering solution that minimizes power consumption while providing reliable real-time performance.

---

## Objectives

The objectives of this project are:

- Design a **32-tap low-pass FIR filter** for ECG denoising.
- Eliminate DSP48 multiplier usage through **shift-and-add arithmetic**.
- Reduce hardware complexity using **symmetric coefficient folding**.
- Improve timing performance using **vertical pipelining**.
- Implement and verify the architecture on an **Artix-7 FPGA**.
- Perform real-time ECG acquisition and visualization using UART communication.
- Evaluate timing, resource utilization, and power consumption.

---

## System Architecture

The complete system consists of four major modules.

### ECG Signal Generation (MATLAB)

- Generates clean ECG waveform.
- Adds high-frequency noise for testing.
- Designs a 32-tap low-pass FIR filter.
- Generates quantized FIR coefficients.
- Exports ECG samples for FPGA simulation.

---

### FPGA Processing Unit

The FPGA performs real-time ECG filtering using a DSP48-free architecture.

#### Delay Line

- Stores the previous ECG samples.
- Provides input samples for FIR computation.

#### Symmetric Pre-Adder

- Exploits coefficient symmetry.
- Reduces the number of multiplication operations.

#### Shift-and-Add Multiplier

- Replaces hardware multipliers using shift and addition operations.
- Eliminates DSP48 block usage.

#### Pipelined MAC Unit

- Performs accumulation in multiple pipeline stages.
- Reduces combinational delay.
- Improves maximum operating frequency.

#### UART Transmitter

- Sends filtered ECG samples to the host computer.
- Enables continuous real-time communication.

---

### Host Computer (Python)

A Python-based application performs:

- UART data acquisition
- Real-time ECG plotting
- Heart-rate estimation
- Live visualization of noisy and filtered ECG signals

---

## Working Principle

1. MATLAB generates noisy ECG samples.
2. ECG samples are provided to the FPGA.
3. Samples pass through the FIR delay line.
4. Symmetric samples are added using the pre-adder stage.
5. Shift-and-add arithmetic performs coefficient multiplication.
6. Pipeline stages accumulate all tap outputs.
7. Filtered ECG samples are transmitted through UART.
8. Python receives and visualizes the ECG waveform in real time.

---

## Design Features

- DSP48-Free FIR Architecture
- 32-Tap Linear Phase FIR Filter
- Symmetric Coefficient Folding
- Shift-and-Add Multiplication
- Vertical Pipelining
- UART-Based Real-Time Streaming
- Low Dynamic Power
- FPGA-Friendly RTL Design

---

## Experimental Results

The implemented design was validated using MATLAB-generated ECG signals with added noise.

The results demonstrate:

- Successful removal of high-frequency noise
- Preservation of ECG waveform morphology
- Stable real-time filtering
- DSP48-free hardware implementation
- Reduced dynamic power consumption
- Successful UART communication with live visualization

Power analysis performed using Vivado indicates a dynamic power consumption of approximately **3 mW** for the optimized implementation.

---

## Conclusion

A low-power 32-tap FIR filter for ECG denoising was successfully designed and implemented on an Artix-7 FPGA. The proposed DSP48-free architecture combines symmetric coefficient folding, shift-and-add multiplication, and vertical pipelining to achieve efficient real-time filtering while reducing hardware resource utilization and dynamic power consumption.

The architecture is suitable for wearable healthcare devices, portable ECG monitoring systems, and other low-power biomedical signal processing applications.

---

## Future Scope

Future improvements include:

- Adaptive FIR filtering for varying noise conditions
- Higher-order FIR filter implementations
- Multi-channel ECG processing
- ASIC implementation for ultra-low-power applications
- Integration with wearable healthcare devices
- Edge AI-assisted ECG anomaly detection

---

## Repository Structure

```text
LowPower-FIR-ECG-Denoising-FPGA/
│
├── rtl/                 # Verilog RTL modules
├── matlab/              # FIR design and coefficient generation
├── python/              # UART interface and ECG visualization
├── simulation/          # Vivado simulation files
├── constraints/         # FPGA XDC files
├── docs/                # Project report, poster, presentation
└── README.md
```

---

## Tools and Technologies

- Xilinx Vivado 2022.2
- Verilog HDL
- MATLAB
- Python 3
- NumPy
- Matplotlib
- PySerial
- Artix-7 FPGA (Basys 3)

---

## License

This project was developed for academic and research purposes as part of an undergraduate engineering project.
