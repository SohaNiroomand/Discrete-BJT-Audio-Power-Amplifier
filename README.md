# 🔊 Discrete BJT Audio Power Amplifier

This project presents the design and LTspice simulation of a fully discrete multi-stage BJT audio amplifier featuring a complementary Class-AB output stage, global negative feedback, and Miller frequency compensation.

The amplifier was designed to drive a \(50\,\Omega\) load while providing high voltage gain, low distortion, good efficiency, and stable operation.

## 📌 Overview

The final circuit includes:

- Differential BJT input stage
- Current mirrors and active loads
- Voltage amplification and driver stages
- Complementary Class-AB push-pull output stage
- Global negative-feedback network
- Miller compensation capacitor
- \(50\,\Omega\) output load

The feedback network uses:

- \(R_f = 200\,k\Omega\)
- \(R_g = 10\,k\Omega\)

The theoretical closed-loop voltage gain is:

\[
A_v = 1+\frac{R_f}{R_g}
=1+\frac{200k}{10k}
=21
\]

## ⚙️ Main Design Parameters

| Parameter | Value |
|---|---:|
| Supply voltage | \(\pm10\,V\) |
| Load resistance | \(50\,\Omega\) |
| Feedback resistors | \(R_f=200\,k\Omega,\ R_g=10\,k\Omega\) |
| Miller capacitor | \(82\,pF\) |
| Standard input | \(50\,mV\) peak at \(1\,kHz\) |
| Large-signal input | \(385\,mV\) peak at \(1\,kHz\) |

## ✅ Final Simulation Results

| Metric | Result | Requirement |
|---|---:|---:|
| Closed-loop gain | 20.877 | 18–22 |
| Output swing | \(16.050\,V_{pp}\) | \(\geq16\,V_{pp}\) |
| Output-stage efficiency | 63.33% | \(>60\%\) |
| THD without noise | 0.040374% | \(<0.08\%\) |
| THD with injected noise | 0.819073% | \(<1\%\) |
| Total power consumption | \(163.76\,mW\) | \(\leq190\,mW\) |
| Input resistance | \(32.48\,M\Omega\) | \(>1\,M\Omega\) |
| Output resistance | \(0.2135\,\Omega\) | \(<50\,\Omega\) |
| PSRR | \(45.43\,dB\) | Reported |
| Estimated circuit cost | 190 | \(\leq200\) |

All mandatory project requirements were satisfied.

## 🧮 Miller Compensation

A Miller capacitor was added around the high-gain voltage-amplification stage to create a dominant pole and improve closed-loop stability.

Using the approximate input-stage transconductance:

\[
g_m \approx \frac{I_C}{V_T}
\approx 2.07\,mS
\]

and targeting a closed-loop bandwidth of approximately \(200\,kHz\):

\[
C_C \approx
\frac{g_m}{2\pi A_{CL}f_{BW}}
\approx 78.9\,pF
\]

The nearest practical value was selected:

\[
C_C=82\,pF
\]

The Miller capacitor improves phase margin and reduces ringing, oscillation, and high-frequency distortion. Increasing its value further improves stability but reduces bandwidth and slew rate.

## 🔁 Effect of Negative Feedback

With global negative feedback, the amplifier produces a clean sinusoidal output with a voltage gain close to 21.

When the feedback network is removed, the large open-loop gain drives the output close to the supply rails and causes severe clipping.

Negative feedback therefore:

- Controls the closed-loop gain
- Improves linearity
- Reduces distortion
- Lowers output resistance
- Stabilizes the operating point
- Improves usable bandwidth

## ⚡ Output Swing and Efficiency

For an input amplitude of \(385\,mV\) at \(1\,kHz\), the amplifier produced:

- Output swing: \(16.050\,V_{pp}\)
- Maximum output voltage: \(8.139\,V\)
- Minimum output voltage: \(-7.911\,V\)
- Average load power: \(644.7\,mW\)
- Output-stage efficiency: 63.33%

No severe clipping was observed at the required output swing.

## 📉 Harmonic Distortion

The total harmonic distortion was measured at the final output node.

- THD without injected noise: **0.040374%**
- THD with injected noise: **0.819073%**

Both results satisfy the project requirements.

## 🎵 Real Audio Signal Test

A personal voice recording was converted to:

- Mono WAV
- 16-bit PCM
- \(44.1\,kHz\) sample rate
- Normalized input amplitude

The input audio was applied in LTspice using:

```text
wavefile="audio.wav" chan=0
```

The amplified output was exported using:

```spice
.wave "output.wav" 16 44100 V(Vout)
```

The measured audio voltage gain was approximately 20.84. No severe clipping was observed, and the input and output FFTs preserved the same main frequency components.

## 🖼️ Selected Results

### Final Circuit

### Audio Input and Output


## 🧪 Tools

- LTspice
- Python
- FFmpeg
- LaTeX / XeLaTeX

## 🧠 Key Takeaways

- Global negative feedback provides accurate gain and improves linearity.
- The Class-AB output stage delivers a large output swing with good efficiency.
- Miller compensation improves stability and phase margin.
- Proper output-stage biasing reduces crossover distortion.
- The final circuit successfully amplifies a real audio signal without severe clipping.

## 👤 Author

**Soha Niroomand**  
Student ID: **403170569**
