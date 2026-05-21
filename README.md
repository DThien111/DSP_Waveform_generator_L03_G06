# Dual-Channel Digital Function Generator & Spectrum Analyzer

A web-based, interactive DSP (Digital Signal Processing) simulation tool built to model a hardware function generator, oscilloscope, and spectrum analyzer. [cite_start]This project provides a real-time visual and auditory showcase of discrete signal theory, telecommunication principles, and hardware design constraints directly within the browser without any external dependencies[cite: 7, 270, 271].

🚀 **Live Demo:** `https://dsp-l03-nhom6.netlify.app/`

---

## 🌟 Key Features

### 1. Independent Dual-Channel Signal Generation (CH1 & CH2)
* [cite_start]Support for 5 fundamental waveforms: Sine, Square, Triangle, Sawtooth, and White Noise[cite: 309, 316, 319, 322].
* [cite_start]Real-time adjustment of **Frequency** ($1\text{ Hz} - 20\text{ kHz}$), **Amplitude** ($0\text{ V} - 20\text{ Vpp}$), and **Initial Phase** ($0^\circ - 360^\circ$)[cite: 316].
* [cite_start]Smart UI Tab switching for clean parameter configuration[cite: 280].

### 2. Dual-Trace Digital Oscilloscope (Time Domain)
* [cite_start]**Dual Trace Rendering:** Displays both CH1 (Yellow) and CH2 (Green) simultaneously using HTML5 Canvas API[cite: 293].
* [cite_start]**Zero-Crossing Trigger Sync:** Implements a software-based trigger synchronized to CH1, locking the wave phase in place for accurate phase shift observations (e.g., demonstrating a $90^\circ$ phase delta)[cite: 294, 334].
* Adjustable Time/Div and Volt/Div scales for custom waveform inspection.

### 3. Spectrum Analyzer (Frequency Domain via FFT)
* [cite_start]**Mixed FFT Visualization:** Computes and overlays the frequency spectrum of both channels using an optimized Radix-2 Fast Fourier Transform algorithm[cite: 218, 297].
* [cite_start]**FDM Telecommunication Demo:** Perfectly visualizes Frequency Division Multiplexing (FDM), showcasing distinct spectral peaks when channels operate on different frequencies[cite: 298, 338, 340].
* [cite_start]Ideal for observing harmonic distributions and the **Gibbs Phenomenon** in non-sinusoidal waves (Square, Triangle, Sawtooth)[cite: 249, 251, 317, 318, 320, 322].

### 4. Real-Time Audio Mixer & Physics Simulation
* [cite_start]Harnesses the browser's **Web Audio API** to synthesize math equations into real physical audio[cite: 274, 285].
* [cite_start]**Phase Delay Simulation:** Converts degree phase shifts into time domain delays via `DelayNode`[cite: 288].
* [cite_start]**Acoustic Wave Interference (Beating):** Generate frequencies with minor deltas (e.g., $1000\text{ Hz}$ and $1005\text{ Hz}$) to experience acoustic beating beats through your speakers[cite: 290, 342, 343].

---

## 🛠️ Built With

* [cite_start]**Frontend Structure:** HTML5 Semantic Elements [cite: 271, 272]
* [cite_start]**Styling & Theme:** CSS3 Grid, Flexbox, custom Sci-Fi/Telecom Cyberpunk theme [cite: 272, 277, 278]
* [cite_start]**Core Logic & DSP Engine:** Vanilla JavaScript (ES6+) [cite: 271, 273]
* [cite_start]**Audio Synthesis:** Web Audio API (`AudioContext`, `OscillatorNode`, `GainNode`, `DelayNode`, `AnalyserNode`) [cite: 274, 287, 288]
* [cite_start]**Graphics Rendering:** HTML5 Canvas API (High-performance animation loop via `requestAnimationFrame`) [cite: 275]

---

## 📐 DSP & Hardware Principles Applied

* [cite_start]**Anti-Aliasing by Design:** To prevent aliasing without analog hardware filters, the UI caps signal inputs at a hard limit of $20\text{ kHz}$[cite: 325, 326]. [cite_start]Paired with the system's high automatic sampling rate ($44.1\text{ kHz}$ to $96\text{ kHz}$), the system inherently satisfies the **Nyquist-Shannon Sampling Theorem** ($f_s \ge 2f_{max}$), guaranteeing mathematically pure reconstruction[cite: 324, 327, 328, 329].
* [cite_start]**Hardware Robustness (Sample Rate Fallback):** Features a robust initialization wrap (`try-catch`). [cite_start]If a device doesn't support high $96\text{ kHz}$ audio processing, it seamlessly fallbacks to the native hardware rate ($44.1\text{ kHz}$ or $48\text{ kHz}$) to ensure stable thread execution.

---

## 📦 How to Run Locally

[cite_start]Since this project is packaged entirely as a lightweight static web app, deployment is zero-config[cite: 301, 303]:

1. Clone or download this repository.
2. [cite_start]Ensure you have your project assets (`index.html`, `logo.png`, `background.jpg`) in the same root folder[cite: 301].
3. Open `index.html` directly inside any modern web browser (Chrome, Edge, Firefox, Safari). **No local web server required!**
