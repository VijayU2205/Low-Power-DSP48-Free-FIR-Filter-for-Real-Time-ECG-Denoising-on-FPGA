# Two-Stage Low-Power FPGA Architecture for Physical-Layer Anomaly Detection in EV Charging Systems

---

## Abstract

Modern EV charging infrastructure is increasingly vulnerable to **physical-layer disturbances** such as electromagnetic interference (EMI), harmonic distortions, and voltage transients. These anomalies can bypass traditional software-based cybersecurity mechanisms and directly impact hardware reliability.

This project presents a **low-power, FPGA-based anomaly detection system** using a **two-stage triage architecture**. The system employs a lightweight **dv/dt and zero-crossing-based hardware filter** for continuous monitoring, combined with an **event-driven autoencoder neural network** for deep inspection. The architecture leverages **clock gating** to activate high-performance processing only when anomalies are suspected, significantly reducing power consumption.

A hardware-in-the-loop setup using dual-laptop communication via UART demonstrates real-time detection and visualization of anomalies. Experimental results validate the system’s ability to detect both high-amplitude transients and low-amplitude stealth harmonics with microsecond latency, making it suitable for next-generation smart grid and EV charging security applications.

---

## Keywords

FPGA, Low-Power Design, Anomaly Detection, Autoencoder, EMI, Harmonics, dv/dt, Physical-Layer Security, Edge AI, EV Charging Systems

---

## Problem Statement

EV charging systems operate on high-power analog signals that are susceptible to **physical-layer disturbances** such as:

* Electromagnetic Interference (EMI)
* High-frequency harmonics
* Voltage spikes and transients
* Phase and waveform distortions

These disturbances can:

* Bypass traditional software-based security systems
* Cause battery degradation or hardware damage
* Lead to instability in smart grid systems

Conventional microcontroller-based monitoring systems are **too slow** to detect these sub-cycle anomalies, necessitating a **real-time hardware-based solution**.

---

## Objectives

The primary objectives of this project are:

* To design a **low-power FPGA-based anomaly detection system**
* To implement a **two-stage triage architecture** for efficient processing
* To detect both **high-amplitude and low-amplitude waveform anomalies**
* To reduce unnecessary power consumption using **clock gating techniques**
* To provide **real-time visualization and monitoring** using a dual-laptop setup
* To support **hardware-in-the-loop simulation for validation**

---

## System Architecture

The proposed system consists of the following major components:

### Input Node (Laptop 1)

* Python-based waveform generator
* Generates:

  * Clean sine wave (normal condition)
  * EMI noise
  * Harmonic distortions
  * Voltage spikes
* Sends data via UART to FPGA

---

### FPGA Processing Unit (Core System)

#### Stage 1: Triage Block (Always ON)

* Operates at ~10 MHz
* Implements:

  * dv/dt (rate of change) detection
  * Zero-crossing jitter analysis
  * Periodic health-check trigger
* Generates wake-up signal for Stage 2

---

#### Stage 2: Autoencoder Block (Event-Driven)

* Operates at ~100 MHz (clock gated using BUFGCE)
* Performs:

  * Signal reconstruction
  * Mean Squared Error (MSE) computation
* Detects anomalies based on reconstruction error

---

#### Clock Gating Unit

* Dynamically enables/disables high-frequency clock
* Reduces power consumption during normal operation

---

#### UART Output Module

* Sends processed data:

  * Original signal
  * Reconstructed signal
  * Anomaly score (MSE)

---

### Output Node (Laptop 2)

* Python-based dashboard
* Displays:

  * Real-time waveform comparison
  * Anomaly detection graph
  * System status (Normal / Attack)

---

## Working Principle

1. Laptop 1 generates and transmits waveform samples to FPGA
2. Stage 1 continuously monitors signal characteristics:

   * If normal → system remains in low-power mode
   * If anomaly suspected → triggers Stage 2
3. Stage 2 autoencoder reconstructs the waveform
4. Reconstruction error (MSE) is calculated
5. If error exceeds threshold:

   * Anomaly is detected
   * Alert signal is generated
6. Results are transmitted to Laptop 2 for visualization

---

## Experimental Results and Discussion

The system was tested using simulated waveform conditions, including:

* Clean sinusoidal signals
* High-frequency EMI noise
* Voltage spikes
* Low-amplitude harmonic distortions

Results demonstrate:

* Accurate detection of both transient and stealth anomalies
* Significant reduction in unnecessary high-power computation
* Fast response time (microsecond-level latency)
* Stable performance across repeated test conditions

---

## Conclusion

This project presents an efficient and scalable **hardware-based anomaly detection system** for EV charging infrastructure. By combining **lightweight triage logic with AI-based deep inspection**, the system achieves:

* High detection accuracy
* Low power consumption
* Real-time response capability

The architecture is well-suited for deployment in **smart grids, EV charging stations, and critical power systems**.

---

## Future Scope

* Integration with real ADC (analog signal acquisition)
* FFT-based frequency-domain anomaly detection
* Multi-channel signal monitoring
* Deployment on real EV charging systems
* AI-based anomaly classification (type identification)
* Integration with smart grid infrastructure

---

##  Repository Structure

```id="structure"
2Stage-LowPower-FPGA-AnomalyDetection-EV/
│
├── rtl/                 # Verilog modules (dv/dt, Autoencoder, UART, Clock Gating)
├── ai/                  # Python scripts for training & quantization
├── scripts/             # Laptop 1 (input) and Laptop 2 (dashboard)
├── testbench/           # Simulation files
├── docs/                # Reports, IEEE paper, diagrams
└── README.md
```

## 📄 License

This project is intended for academic and research purposes.
