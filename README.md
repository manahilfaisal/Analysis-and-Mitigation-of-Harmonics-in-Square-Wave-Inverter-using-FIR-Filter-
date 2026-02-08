
# Inverter Harmonic Analysis and Filtering in MATLAB

## Overview

This project simulates a **DC-to-AC inverter output**, analyzes its harmonic content, filters the signal to generate a **pure sine wave**, and calculates the **Total Harmonic Distortion (THD)** before and after filtering. The code also verifies compliance with **IEEE-519 standards** for harmonic distortion.  

**Objectives:**

- Generate a **square-wave AC signal** representing inverter output.  
- Perform **FFT analysis** to visualize harmonics.  
- Design and apply a **FIR low-pass filter** to remove higher-order harmonics.  
- Compute and compare **THD** before and after filtering.  
- Check **IEEE-519 compliance**.

---

## Features

- **Square-Wave Signal Generation**: Models the output of a simple inverter.  
- **Harmonic Analysis**: Extracts the first 7 odd harmonics and their magnitudes.  
- **THD Calculation**: Measures signal distortion in percentage.  
- **Filtering**: Converts square wave to nearly pure sine wave using a **FIR low-pass filter**.  
- **Visualization**: Plots time-domain signals, frequency spectra, and harmonic bar charts.  
- **Compliance Check**: Automatically verifies **IEEE-519 standard** for THD (<5%).

---

## Requirements

- MATLAB (R2016b or later recommended)  
- Signal Processing Toolbox  

---

## Code Structure

### 1. Signal Generation
```matlab
Fs = 5000;          % Sampling frequency
t = 0:1/Fs:0.5;     % Time vector
f0 = 50;            % Fundamental AC frequency
Vpeak = 378;        % Square wave amplitude

x = Vpeak * square(2*pi*f0*t);  % Inverter output
````

* Generates a **50 Hz square wave** with peak voltage 378 V.
* Represents typical **DC-to-AC inverter output**.

---

### 2. FFT and Harmonic Analysis

```matlab
N = length(x);
X = fft(x);
f = (0:N-1)*(Fs/N);
X_mag = abs(X)/N;
```

* Computes **FFT of square wave** to extract frequency components.
* Harmonics extracted: 1st, 3rd, 5th, … 15th.
* Displays **harmonic table** and plots **bar chart**.

---

### 3. Total Harmonic Distortion (THD)

```matlab
V1 = V(1);
THD_before = sqrt(sum(V(2:end).^2))/V1 * 100;
```

* THD formula: THD = (sqrt(V_2^2 + V_3^2 + ... + V_N^2)) / V_1 * 100%


* Quantifies distortion of the square wave relative to fundamental.

---

### 4. FIR Low-Pass Filtering

```matlab
fc = 60;                  % Cutoff frequency slightly above fundamental
Wn = fc/(Fs/2);
b_fir = fir1(120, Wn);
y_filtered = filter(b_fir, 1, x);
```

* Converts square wave into a **near-pure sine wave**.
* Removes harmonics above cutoff frequency.

---

### 5. Post-Filtering Analysis

* Computes **FFT** of filtered signal.
* Extracts harmonic magnitudes after filtering.
* Calculates **THD_after**.
* Checks **IEEE-519 compliance**:

```matlab
if THD_after < 5
    disp('IEEE-519 Compliance: PASS')
else
    disp('IEEE-519 Compliance: FAIL')
end
```

---

## Plots Generated

1. **Time-Domain Square Wave**
2. **FFT of Original Signal** (Before Filtering)
3. **Bar Chart of Harmonics** (Before Filtering)
4. **Filtered Sine Wave**
5. **FFT of Filtered Signal**
6. **Bar Chart of Harmonics After Filtering**
7. **THD Comparison** (Before vs After Filtering)

---

## Results

* **Harmonics**: Only the odd harmonics are significant in the square wave.
* **THD Before Filtering**: High (~40-50% typical for square wave).
* **THD After Filtering**: Drastically reduced (~<5%).
* **IEEE-519 Compliance**: Achieved after FIR low-pass filtering.
* **Detailed Results**:[Inverter Harmonic Analysis and FIR Filtering Using MATLAB](Inverter_Harmonic_Analysis_Report.pdf)

---




