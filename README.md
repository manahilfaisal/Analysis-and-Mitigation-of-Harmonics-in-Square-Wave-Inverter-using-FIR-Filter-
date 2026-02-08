

# Analysis and Mitigation of Harmonics in Square Wave Inverter 

This project demonstrates the generation of an AC sine wave from a DC source using a square wave inverter and FIR low-pass filtering in MATLAB. The simulation calculates harmonics, THD (Total Harmonic Distortion), and verifies IEEE-519 compliance.

---

## Features
* **DC → AC Generation:** Generates a square wave with defined amplitude.
* **FIR Filtering:** Applies a Finite Impulse Response low-pass filter to produce a near-pure sine wave.
* **Automated Analysis:**
    * Time-domain waveforms for square and filtered signals.
    * FFT visualization of harmonics.
    * Harmonic magnitude tables (first 7 odd harmonics).
    * THD computation before and after filtering.
* **Compliance Check:** Verifies THD against IEEE-519 limits for AC systems.

---

## Signal Characteristics
The simulation is calibrated for standard household AC output.

| Parameter | Square Wave (Input) | Filtered Sine Wave |
| :--- | :--- | :--- |
| **Peak Voltage** | 378V | ~311V |
| **RMS Voltage** | 267V | ~220V |

### Key Notes on Filtered Sine Peak
The reduction from 378V square wave to 311V sine peak is expected and due to:
* **Fundamental extraction:** The amplitude of the fundamental frequency component.
* **Filter attenuation:** FIR filter characteristics in the passband.
* **RMS Verification:** $V_{RMS} = \frac{V_{peak}}{\sqrt{2}}$ matches standard 220V household levels.



---

## MATLAB Code Overview

### Parameters
* `Fs`: Sampling frequency
* `f0`: AC fundamental frequency
* `Vpeak`: Square wave amplitude (DC source voltage)
* `fc`: Cutoff frequency of the FIR low-pass filter

### Core Implementation
```matlab
% Square Wave Generation
x = Vpeak * square(2*pi*f0*t);

% FIR Filtering (120th Order)
b_fir = fir1(120, Wn);
y_filtered = filter(b_fir, 1, x);

```

### THD and Harmonics

The first 7 odd harmonics are extracted and displayed in MATLAB tables. THD is computed as:

---

## Visualizations Generated

1. **Time-domain waveform** of the original square wave.
2. **FFT and harmonic bar plot** before filtering.
3. **Time-domain waveform** of the filtered sine wave (~311V peak).
4. **FFT and harmonic bar plot** after filtering.
5. **THD comparison** before and after filtering.

---

## Usage

1. Open MATLAB and create a new `.m` file.
2. Set desired `Vpeak`, `Fs`, `f0`, and filter cutoff `fc`.
3. Run the script to generate all plots, tables, and THD analysis.

## Project Files

* `inverter_square_to_sine.m`: MATLAB code.
* `simulation_report.pdf`: Detailed analysis and IEEE-519 compliance report.

```

