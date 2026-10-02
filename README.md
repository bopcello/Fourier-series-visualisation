# 🌀 Fourier Series & Epicycles Interactive Laboratory

> **An interactive, zero-dependency, browser-native laboratory for visualizing Fourier series decomposition, epicyclic phasor synthesis, frequency spectra, and harmonic analysis.**

---

## 📌 Overview

The **Fourier Series & Epicycles Interactive Laboratory** is a comprehensive educational visualization platform designed to bridge abstract mathematical analysis with physical and geometric intuition. By rendering the Fourier decomposition as a cascade of rotating epicycles (complex phasors in $\mathbb{C}$ or $\mathbb{R}^2$), students and educators can visually trace how individual sinusoidal harmonics sum constructively and destructively to reconstruct complex waveforms.

Built entirely with standard web technologies (HTML5 Canvas and Vanilla JavaScript), the laboratory runs instantly in any modern web browser without dependencies, package managers, server setups, or internet connectivity.

---

## 🎓 Academic Utility & Pedagogical Framework

Fourier analysis is a foundational pillar across mathematics, physics, electrical engineering, computer science, and acoustics. However, students frequently struggle to transition from symbolic integration formulas to an intuitive understanding of harmonic superposition, phase alignment, and spectral decay.

This application is designed specifically as an **in-class lecture companion**, an **interactive laboratory exploration workbench**, and a **homework self-validation tool**.

### 1. Demystifying Complex Phasors & Epicycles
* **Euler’s Formula in Motion:** Epicycles visually demonstrate $e^{i n \omega_0 t} = \cos(n \omega_0 t) + i \sin(n \omega_0 t)$. Each circle represents a harmonic frequency with radius equal to harmonic amplitude and angular velocity proportional to $n$.
* **Concentric vs. Chained Phasors:** The toggleable *Concentric Mode* re-centers all circles to the origin, allowing students to observe isolated phase angles and amplitudes without the visual compounding of chained vector addition.
* **Synchronized State Inspection:** Toggling **Animate** immediately freezes both epicyclic rotation and waveform scrolling simultaneously, allowing instructors to halt the system at any critical phase angle (e.g., $t = 0, \pi/2, \pi$) to inspect vector contributions term-by-term.

### 2. Multi-Perspective Harmonic Representations
The **Coefficient Laboratory** allows students to toggle between the four standard textbook representations of Fourier series for any function:
1. **Trigonometric Form:** $f(x) \approx a_0 + \sum_{n=1}^{N} \left[ a_n \cos(2\pi n x) + b_n \sin(2\pi n x) \right]$
2. **Compact Polar / Harmonic Form:** $f(x) \approx c_0 + \sum_{n=1}^{N} c_n \cos(2\pi n x + \varphi_n)$, emphasizing amplitude-phase relationships.
3. **Complex Exponential Form:** $f(x) \approx \sum_{n=-N}^{N} c_n e^{i 2\pi n x}$, showing negative frequency symmetry ($c_{-n} = c_n^*$).
4. **Half-Range Expansions (Sine & Cosine):** Demonstrating even and odd periodic extensions over $[0, L]$.

### 3. Understanding Symmetry & Vanishing Coefficients
Students can verify Dirichlet symmetry rules in real time:
* **Even Functions** ($f(-x) = f(x)$): $b_n = 0$, reconstructed exclusively via cosine terms.
* **Odd Functions** ($f(-x) = -f(x)$): $a_n = 0$, reconstructed exclusively via sine terms.
* **Half-Wave Symmetry** ($f(x + T/2) = -f(x)$): Even harmonics vanish ($a_{2k} = b_{2k} = 0$), retaining only odd harmonics ($n = 1, 3, 5, \dots$).

### 4. Direct Observation of Spectral Decay
* **Discontinuous Signals (Square, Sawtooth):** Coefficients decay at $\mathcal{O}(1/n)$, leading to slow convergence and sharp high-frequency ripples.
* **Continuous but Non-Differentiable Signals (Triangle):** Coefficients decay at $\mathcal{O}(1/n^2)$, demonstrating dramatically faster convergence with fewer audible/visible harmonics.
* **Smooth Signals:** Exponential or finite-term spectral decay.

### 5. Parseval’s Theorem & Energy Conservation
* Real-time calculation of cumulative signal power across harmonics:
  $$\frac{1}{T} \int_0^T |f(t)|^2\,dt = \sum_{n=-\infty}^{\infty} |c_n|^2 = a_0^2 + \frac{1}{2}\sum_{n=1}^\infty (a_n^2 + b_n^2)$$
* Displays exact energy capture percentages (e.g., $90\%$, $95\%$, $99\%$) as harmonic cutoff $N$ varies.

---

## 🔬 Advanced Academic Capabilities

### ✍️ 1. Custom Waveforms: Equation Parser & Freehand Sketchpad
Beyond standard canonical signals, students can explore arbitrary custom signals:
* **Math Expression Engine:** Supports arbitrary continuous and piecewise functions defined over $x \in [0, 1]$. Enter ternary piecewise statements (`x < 0.5 ? 1 : -1`), polynomials (`x*x`), exponentials (`exp(2*x)`), Bessel series (`exp(0.8*cos(2*pi*x))`), or transcendental combinations.
* **Interactive Waveform Sketchpad:** An in-browser drawing modal allows instructors and students to sketch arbitrary curves using mouse or touch input. The sketchpad features real-time coordinate normalization, spline/moving-average curve smoothing, and a 1,024-point discretization pipeline that instantly decomposes hand-drawn shapes into Fourier harmonics.

### ⚡ 2. Automatic Discontinuity Detection (Gibbs Phenomenon Inspector)
Real signals often contain jump discontinuities that trigger ringing artifacts. The laboratory includes an automated discontinuity analyzer:
* **Autonomous High-Resolution Jump Scanner:** For custom and hand-drawn waveforms, the engine scans $1,024$ discrete sample points across the period—including the periodic boundary wrap at $x = 0 \leftrightarrow 1$—to detect sharp step transitions ($\Delta y \ge 0.35$).
* **Dynamic Discontinuity Localization:** It precisely pinpoints the discontinuity location ($x_\text{jump}$), step size, and left/right plateau levels.
* **Empirical vs. Theoretical Overshoot Comparison:** Automatically focuses the Gibbs analysis window around the detected discontinuity and evaluates the high-resolution reconstructed series over $600$ points to measure the empirical peak overshoot percentage.
* **Wilbraham–Gibbs Benchmark:** Displays the theoretical limit alongside the empirical result:
  $$\Delta = \frac{1}{\pi} \int_0^\pi \frac{\sin t}{t}\,dt - \frac{1}{2} \approx 8.9490\%$$
* **Continuous Signal Guard:** If a waveform is smooth or continuous (such as a pure sine or triangle wave), the system flags it as `0.00% (Continuous wave)`, reinforcing that Gibbs ringing occurs strictly at jump discontinuities.

### 📐 3. Piecewise & Analytical $a_n, b_n, c_n$ Calculations
When studying piecewise or numerically evaluated signals, traditional visualizers only display opaque decimal numbers. This laboratory dynamically generates **evaluated piecewise mathematical formulations** rendered in textbook-quality $\LaTeX$:
* **Piecewise Trigonometric Cases:** Formulates $a_n$ and $b_n$ in standard piecewise case notation:
  $$a_n \approx \begin{cases} \text{value}, & n = 1 \\ \text{value}, & n = 3 \\ 0, & \text{otherwise} \end{cases} \qquad b_n \approx \begin{cases} \text{value}, & n = 1 \\ \text{value}, & n = 3 \\ 0, & \text{otherwise} \end{cases}$$
* **Complex Exponential Coefficients ($c_n, c_{-n}$):** Automatically separates real and imaginary components ($c_n = \frac{a_n}{2} - i\frac{b_n}{2}$, $c_{-n} = \frac{a_n}{2} + i\frac{b_n}{2}$) and presents them alongside the DC offset $c_0$.
* **Half-Range Sine & Cosine Systems:** Automatically computes and displays the half-range expansion cases over $[0, L]$.
* **Offline Typography Engine:** Formatted using a pure CSS/JavaScript layout engine with optional KaTeX acceleration—guaranteeing crisp mathematical formulas without requiring an active internet connection.

---

## 🚀 Feature Matrix

| Feature | Description |
| :--- | :--- |
| **Real-time Epicycle Rendering** | Smooth HTML5 canvas vector rendering at 60 FPS with harmonic coloring and dynamic radius scaling. |
| **Synchronous Freeze/Pause** | Freezes epicycle rotations and wave scrolling in unison for static classroom analysis. |
| **Concentric Circle Toggle** | Morphing animation between tip-to-tail chained epicycles and centered concentric phasors. |
| **Comprehensive Waveform Library** | Built-in presets for Square, Sine, Triangle, Sawtooth, and variable Duty Cycle Pulse Trains. |
| **Custom Equation Parser** | Live evaluation of piecewise expressions (`x < 0.5 ? 1 : -1`), Bessel series, polynomials, and transcendentals. |
| **Freehand Waveform Sketchpad** | Interactive mouse/touch drawing modal with curve smoothing to analyze custom periodic shapes. |
| **Automatic Discontinuity Detector** | High-speed 1,024-point jump scanner locating discontinuities and calculating empirical Gibbs overshoot. |
| **Piecewise Coefficient Generator** | Generates formal $\LaTeX$ piecewise case statements for $a_n, b_n, c_n, c_{-n}$ across all expansion bases. |
| **Amplitude & Phase Spectrum Panels** | Autoscaled bar charts displaying $|c_n|$ and $\varphi_n = \text{atan2}(-b_n, a_n)$ with modal expansion dialogs. |
| **Analytical & Decimal Coefficients** | Switch between exact symbolic formulas (fractions, $\pi$ multiples) and 4-decimal floating point values. |
| **Gibbs Discontinuity Inspector** | Isolated zoomed view tracking ringing oscillations and peak overshoot percentage. |
| **Dark & Light Mode** | High-contrast presentation-ready themes with persistent state via `localStorage`. |
| **Fully Offline & Self-Contained** | Zero external CDNs or build tooling required; standalone single-file distribution. |

---

## 🛠️ Classroom Lesson Plans & Activities

### 🔬 Activity 1: The Geometry of Harmonic Addition
* **Objective:** Understand how circular motion generates sinusoidal waves.
* **Procedure:**
  1. Select **Sine Wave** with `Terms = 1`.
  2. Observe the single circle tracing out a pure sinusoidal wave on the right.
  3. Switch to **Square Wave** and increment `Terms` from $1$ to $3$, $5$, and $15$.
  4. Note that each added epicycle has a smaller radius ($\propto 1/n$) and rotates at odd integer multiples of the fundamental frequency ($3\omega, 5\omega, 7\omega, \dots$).

### 🔬 Activity 2: Investigating the Gibbs Phenomenon & Auto-Detection
* **Objective:** Analyze convergence behavior at jump discontinuities in preset and custom functions.
* **Procedure:**
  1. Select **Square Wave** and open the **Gibbs Phenomenon** panel.
  2. Increase `Number of Terms` from $5$ to $50$ to $100$.
  3. Observe that the frequency of oscillations near the jump increases, compressing against the discontinuity, yet the peak overshoot remains fixed at $\approx 8.95\%$.
  4. Switch to **Custom Equation** and enter a custom step: `x < 0.3 ? 1.5 : -0.5`.
  5. Observe how the **Auto-Discontinuity Detector** automatically locates the jump at $x = 0.3$, centers the analysis window, and extracts the empirical ringing overshoot.

### 🔬 Activity 3: Pulse Width Modulation (PWM) & Spectral Nulls
* **Objective:** Connect Fourier series to PWM signals used in power electronics and telecommunications.
* **Procedure:**
  1. Select **Pulse Train** and adjust the **Duty Cycle** slider from $10\%$ to $50\%$ to $90\%$.
  2. Open the **Amplitude Spectrum** panel and observe how harmonic nulls (zero-crossings of the $\text{sinc}$ envelope) shift depending on duty ratio $D = \tau/T$.
  3. Verify that at $D = 50\%$, all even harmonics vanish, recovering the classic square wave spectrum.

### 🔬 Activity 4: Freehand Waveform Drawing & Harmonic Synthesis
* **Objective:** Discover how arbitrary real-world shapes decompose into sinusoidal spectra.
* **Procedure:**
  1. Click **Draw an Equation** to open the sketchpad modal.
  2. Draw an asymmetric pulse, an electrocardiogram (ECG) approximation, or an arbitrary wave profile.
  3. Click **Smooth Wave** and **Apply Drawn Waveform**.
  4. Inspect the **Piecewise Coefficient Laboratory** to examine the resulting $a_n, b_n$ breakdown and observe how the epicycles reconstruct the drawn geometry.

---

## 🎛️ Controls & Shortcuts

* **Number of Terms Slider ($1 - 100$):** Sets harmonic cutoff order $N$.
* **Animation Speed Slider ($0.1\times - 3.0\times$):** Modulates simulation angular velocity.
* **Scale Slider ($0.3\times - 2.0\times$):** Vertically scales epicycles and waveform trace.
* **Animate Checkbox:** Pauses/resumes epicycle rotation and graph scrolling in lockstep.
* **Concentric Circles Checkbox:** Morphs epicycles into origin-centered phasors.
* **Show Decimal Checkbox:** Toggles coefficient cards between analytical format and numerical decimals.
* **Expand Buttons ($\ne$):** Opens modal inspector views for Amplitude Spectrum, Phase Spectrum, and Coefficient Tables.
* **Theme Toggle:** Switches between Obsidian Dark and High-Contrast Academic Light themes.

---

## 📂 Project Structure

```text
Fourier-series-visualisation/
├── index.html       # Self-contained application (UI, Math, Canvas Engine, Styles)
└── README.md        # Documentation and academic reference guide
```

---

## 💻 Technical Implementation Details

* **Single-File Architecture:** The entire application resides in [`index.html`](file:///d:/Experiments/fs%20vis/Fourier-series-visualisation/index.html), combining responsive layout styling, an optimized vector canvas pipeline, an expression tokenizer, and dynamic matrix/vector solvers.
* **Rendering Loop:** Uses `requestAnimationFrame` with double-buffered canvas transformations, coordinate origin offsets, and an adaptive trace buffer (`maxWavePoints = 1200`).
* **Frame-Synchronous State Flushing:** Modifying coefficients or waveform presets schedules an atomic buffer flush on the subsequent frame boundary, eliminating visual tearing and invalid interpolation artifacts.
* **Numerical Quadrature Engine:** Custom equations and hand-drawn waveforms are computed using high-resolution Riemann/trapezoidal quadrature across 1,024 sample points per period to guarantee coefficient convergence.
* **Dynamic Jump Analysis:** Vectorized jump-difference scanning ($\Delta y$) over periodic boundary wraps to handle periodic continuity seamlessly.

---

## 📖 Recommended Courses & Applications

* **Calculus II / Advanced Engineering Mathematics:** Orthogonal series, boundary value problems, Sturm–Liouville theory.
* **Signals & Systems / DSP (Digital Signal Processing):** Continuous-time Fourier series (CTFS), frequency domain filtering, spectral analysis.
* **Physics & Vibrations:** Normal modes, harmonic oscillators, acoustics, wave propagation.
* **Telecommunications:** Modulation, bandwidth allocation, pulse shaping, harmonic distortion.

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE). Academic redistribution, classroom presentation, and educational derivative works are encouraged.