# Dual-Channel Digital Function Generator & Spectrum Analyzer

A web-based, interactive DSP (Digital Signal Processing) simulation tool built to model a hardware function generator, oscilloscope, and spectrum analyzer. This project provides a real-time visual and auditory showcase of discrete signal theory, telecommunication principles, and hardware design constraints directly within the browser without any external dependencies.

🚀 **Live Demo:** `https://dsp-l03-nhom6.netlify.app/`

---

## 🌟 Key Features

### 1. Independent Dual-Channel Signal Generation (CH1 & CH2)
* Support for 5 fundamental waveforms: Sine, Square, Triangle, Sawtooth, and White Noise
* Real-time adjustment of **Frequency** ($1\text{ Hz} - 20\text{ kHz}$), **Amplitude** ($0\text{ V} - 20\text{ Vpp}$), and **Initial Phase** ($0^\circ - 360^\circ$)
* Smart UI Tab switching for clean parameter configuration

### 2. Dual-Trace Digital Oscilloscope (Time Domain)
* **Dual Trace Rendering:** Displays both CH1 (Yellow) and CH2 (Green) simultaneously using HTML5 Canvas API
* **Zero-Crossing Trigger Sync:** Implements a software-based trigger synchronized to CH1, locking the wave phase in place for accurate phase shift observations (e.g., demonstrating a $90^\circ$ phase delta)
* Adjustable Time/Div and Volt/Div scales for custom waveform inspection.

### 3. Spectrum Analyzer (Frequency Domain via FFT)
* **Mixed FFT Visualization:** Computes and overlays the frequency spectrum of both channels using an optimized Radix-2 Fast Fourier Transform algorithm
* **FDM Telecommunication Demo:** Perfectly visualizes Frequency Division Multiplexing (FDM), showcasing distinct spectral peaks when channels operate on different frequencies
* Ideal for observing harmonic distributions and the **Gibbs Phenomenon** in non-sinusoidal waves (Square, Triangle, Sawtooth)

### 4. Real-Time Audio Mixer & Physics Simulation
* Harnesses the browser's **Web Audio API** to synthesize math equations into real physical audio
* **Phase Delay Simulation:** Converts degree phase shifts into time domain delays via `DelayNode`
* **Acoustic Wave Interference (Beating):** Generate frequencies with minor deltas (e.g., $1000\text{ Hz}$ and $1005\text{ Hz}$) to experience acoustic beating beats through your speakers
---

## 🛠️ Built With

* **Frontend Structure:** HTML5 Semantic Elements 
* **Styling & Theme:** CSS3 Grid, Flexbox, custom Sci-Fi/Telecom Cyberpunk theme 
* **Core Logic & DSP Engine:** Vanilla JavaScript (ES6+) 
* **Audio Synthesis:** Web Audio API (`AudioContext`, `OscillatorNode`, `GainNode`, `DelayNode`, `AnalyserNode`)
* **Graphics Rendering:** HTML5 Canvas API (High-performance animation loop via `requestAnimationFrame`) 
---

## 📐 DSP & Hardware Principles Applied

* **Anti-Aliasing by Design:** To prevent aliasing without analog hardware filters, the UI caps signal inputs at a hard limit of $20\text{ kHz}$. Paired with the system's high automatic sampling rate ($44.1\text{ kHz}$ to $96\text{ kHz}$), the system inherently satisfies the **Nyquist-Shannon Sampling Theorem** ($f_s \ge 2f_{max}$), guaranteeing mathematically pure reconstruction.
* **Hardware Robustness (Sample Rate Fallback):** Features a robust initialization wrap (`try-catch`). If a device doesn't support high $96\text{ kHz}$ audio processing, it seamlessly fallbacks to the native hardware rate ($44.1\text{ kHz}$ or $48\text{ kHz}$) to ensure stable thread execution.

---

## 📦 How to Run Locally

Since this project is packaged entirely as a lightweight static web app, deployment is zero-config:

1. Clone or download this repository.
2. Ensure you have your project assets (`index.html`, `logo.png`, `background.jpg`) in the same root folder
3. Open `index.html` directly inside any modern web browser (Chrome, Edge, Firefox, Safari). **No local web server required!**
