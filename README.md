# Cascaded-AD603-Wideband-VGA

Two-Stage Cascaded AD603 Wideband Variable Gain Amplifier (VGA) with linear-in-dB control, migrated from OrCAD/PSpice to eSim under the FOSSEE Research Migration Project.

---

## Research Migration Project (FOSSEE, IIT Bombay)

This repository is part of the **Research Migration Project** by FOSSEE, IIT Bombay:  
https://esim.fossee.in/research-migration-project

The initiative promotes reproducing published research circuits in **eSim** (open-source), especially those originally implemented in proprietary tools.

---

## Participant Details

- **Name:** Karnati Giridhar Reddy  
- **Affiliation:** Department of Electronics and Communication Engineering,  
  Chaitanya Bharathi Institute of Technology (CBIT), Hyderabad, Telangana, India

---

## Circuit Title

**Two-Stage Cascaded AD603 Wideband Variable Gain Amplifier with Linear-in-dB Control**

---

## Theory / Description

The AD603 (Analog Devices) is a voltage-controlled VGA with:

- Low input-referred noise (~1.3 nV/√Hz)
- Wide bandwidth (~90 MHz)
- Linear-in-dB gain control

A single AD603 supports about **40 dB gain range**.  
To achieve **80 dB total range (10,000×)**, two AD603 stages are cascaded.

### Operating concept

- Input signal enters through **R1 = 100 Ω** into Stage 1 (U3)
- Stage 1 output drives Stage 2 (U4)
- Final output is taken from pin 7 of U4 through **C1 = 22 µF** to a **1 kΩ** load
- A common control voltage **VC (0–2 V)** is applied to pin 1 of both AD603 ICs
- Control sensitivity is **25 mV/dB** across the cascade

### Gain mapping

- **VC = 0 V → 0 dB**
- **VC = 1 V → 40 dB**
- **VC = 2 V → 80 dB**

### Supply and bias

- ±9 V rails
- 2.5 V reference
- Feedback and gain partitioning with:
  - **R3, R7 = 2.49 kΩ**
  - **R8 = 5.1 kΩ (SET = 0.42)**
  - **R9 = 6.2 kΩ (SET = 0.2906)**

---

## Why Reproduce in eSim?

1. Original implementation uses licensed proprietary software (OrCAD/PSpice); eSim makes the design freely accessible.
2. The circuit is relevant for analog/RF education (cascaded VGA behavior, linear-in-dB control, bandwidth studies).
3. AD603 model integration in eSim builds reusable open-source SPICE resources.
4. Reproducing published PSpice behavior in eSim validates both design and toolchain for practical applications (radar, SDR, AGC, biomedical instrumentation).

---

## Expected Analyses and Outcomes

### 1) Transient Analysis

- Input: 1 mV, 1 kHz sine
- Simulation: 0.1 s, max step 20 µs
- Expected output: amplified sine, about **3.28 V peak** (near default VC ≈ 1.85 V)

### 2) AC Sweep (Bode Plot)

- Sweep: 100 Hz to 500 MHz (100 points/decade)
- Expected: ~70 dB flat midband gain, roll-off beyond ~21 MHz

### 3) Parametric Sweep (Gain vs Control Voltage)

- Sweep VC from 0 to 2 V
- Expected linear gain relation:
  - 0 V → 0 dB
  - 1 V → 40 dB
  - 2 V → 80 dB
- Slope: **40 dB/V**

All simulation outputs are to be compared against reference PSpice results from the cited paper.

---

## Repository Structure

- `README.md` – Project overview and migration context
- `Summary/2stageAD603VGAGiridhar.pdf` – Project summary/report
- `eSim simulations/` – eSim-related simulation files

---

## Reference Paper

- **Title:** Modeling and Its Simulation of AD603 based on PSpice software  
- **Authors:** Guo Zipeng, Xiao Yongjun  
- **Venue:** 2011 International Conference on Consumer Electronics, Communications and Networks (CECNet)  
- **Pages:** 2330–2333  
- **ISBN:** 978-1-61284-459-6

---

## Additional References

1. AD603 Datasheet (Analog Devices): https://www.analog.com/en/products/ad603.html  
2. eSim Documentation (FOSSEE, IIT Bombay): https://esim.fossee.in/  
3. Sedra & Smith, *Microelectronic Circuits*  
4. Tang Yanfeng et al., “Design of numeric control, high-gain and wide bandwidth amplifier based on AD603,” *Journal of Changchun University of Science and Technology*, Vol. 33, pp. 81–83, Mar. 2010  
5. Wu Jianbin, Tian Mao, “Implementation of time varying gain amplifier based on the AD603,” *Electronic Measurement Technology*, Vol. 31, pp. 29–32, Apr. 2008

---

## Notes

This project reproduces and migrates a validated AD603 cascade design to open-source simulation infrastructure and serves as a reusable educational/research resource.
