
# 4th Order Sallen-Key Active Low-Pass Filter for Biomedical Applications

## 🎯 Project Overview
This project implements a 4th-order active low-pass filter using the Sallen-Key topology, designed for biomedical signal processing applications (PPG, ECG, EMG, Gait Analysis). The filter is simulated using **eSim 2.5** with **NGSpice 35** and **KiCad 6**.

**Cutoff Frequency:** ~59 Hz  
**Roll-off Rate:** -80 dB/decade  
**Op-Amp:** LM324 (Dual ±12V supply)  

## 📋 Key Specifications
| Parameter | Value |
|-----------|-------|
| Filter Type | 4th Order Sallen-Key Low-Pass |
| Cutoff Frequency (f₀) | ~59 Hz |
| Passband Gain | ~0 dB |
| Stopband Attenuation (1 kHz) | ~-80 dB |
| Q-factor (Stage 1) | 0.5412 |
| Q-factor (Stage 2) | 1.3066 |
| Power Supply | ±12V DC |

## 🔬 Simulation Results
### Frequency Response (Bode Plot)
[View Bode Plot](results/simulation_Frequency Response (Bode Plot).pdf)
- Flat passband up to ~59 Hz
- Steep -80 dB/decade roll-off

### Transient Response (50 Hz Passband)
[View Transient Response](results/Transient_Analysis_50Hz.pdf)
- Clean sinusoidal output at 50 Hz
- Amplitude ~4.2V peak

### Noise Rejection (1 kHz Stopband)
[View Noise Rejection](results/4th_Order_LPF_Noise_Rejection_1kHz.pdf)
- Complete attenuation of 1 kHz signal
- Output ~0V

## 🛠️ Tools Used
- **eSim 2.5** - Open-source EDA tool
- **NGSpice 35** - Circuit simulation engine
- **KiCad 6** - Schematic capture

## 📁 Repository Structure
```
├── docs/          # Documentation and reports
│   └── abstractreport4thOrderLPF.pdf
├── schematic/     # KiCad schematic files
│   ├── LPF_4th_Order_Migration.kicad_sch
│   ├── LPF_4th_Order_Migration.kicad_pro
│   ├── LPF_4th_Order_Migration.net
│   └── lmx24_lm2902.kicad_sym
├── simulation/    # NGSpice netlist and simulation files
│   └── LPF_4th_Order_Migration.cir
├── models/        # SPICE models for components
│   ├── lm324.lib
│   ├── LM324.sub
│   └── lmx24_lm2902.lib
├── results/       # Simulation result images
│   ├── bode_plot.png
│   ├── transient_50Hz.png
│   └── noise_rejection_1kHz.png
├── README.md
├── LICENSE
└── .gitignore
```

## 🚀 How to Run
1. Install [eSim](https://esim.fossee.in/) from FOSSEE, IIT Bombay
2. Clone this repository:
   ```bash
   git clone https://github.com/Tooba-imtiyaz/4th-Order-LPF-Biomedical-Filter.git
   ```
3. Open eSim and load the project:
   - File → Open Project
   - Navigate to `schematic/LPF_4th_Order_Migration.kicad_pro`
4. Run simulation using NGSpice:
   - Click on "Simulate" button in eSim
   - Select AC Analysis for frequency response
   - Select Transient Analysis for time-domain signals
5. View results in eSim waveform viewer

## 📊 Component Values
| Component | Value | Function |
|-----------|-------|----------|
| R1, R2 | 27kΩ | Stage 1 input resistors |
| R3, R5 | 27kΩ | Stage 2 filter resistors |
| VR1 | 22kΩ | Variable potentiometer (tuning) |
| R4 | 9.1kΩ | Stage 2 lower feedback resistor |
| R5 (feedback) | 15kΩ | Stage 2 upper feedback resistor |
| C1, C2, C4 | 0.1μF | Filter capacitors |
| C3, C5 | 0.1μF | Bypass/feedback capacitors |
| U1, U2 | LM324 | Op-amp (VCC=+12V, VEE=-12V) |
| v1 | 1V AC | Input signal source |
| v2, v3 | 12V DC | Dual symmetric power supply |

## 📖 Theory
The Sallen-Key topology, introduced by R.P. Sallen and E.L. Key (1955), is a widely used Voltage Controlled Voltage Source (VCVS) active filter configuration. It realizes second-order transfer functions using a single operational amplifier with two passive RC sections and positive feedback.

The standard second-order Sallen-Key low-pass transfer function is:

**H(s) = ω₀² / (s² + (ω₀/Q)s + ω₀²)**

where ω₀ = 2πf₀ is the natural angular frequency and Q is the quality factor.

A fourth-order low-pass filter is realized by cascading two second-order stages. The overall transfer function H(s) = H₁(s) × H₂(s) yields a roll-off of -80 dB/decade — far steeper than first-order (-20 dB/decade) or second-order (-40 dB/decade) filters.

For a Butterworth response, the pole Q values are:
- **Q₁ = 0.5412** (Stage 1, Sallen-Key)
- **Q₂ = 1.3066** (Stage 2, conventional 2nd order)

The cutoff frequency per stage is:
**f₀ = 1 / (2πRC) = 1 / (2π × 27000 × 0.0000001) ≈ 59 Hz**

## 🎯 Applications
This filter is specifically designed for biomedical applications targeting very low frequencies:
- **PPG (Photoplethysmography):** 0.5-5 Hz
- **Gait Analysis:** 0-15 Hz
- **Cardiac Auscultation:** 20-420 Hz
- **EMG (Electromyography):** 50-150 Hz

## 📚 References
1. Burman, K., Bag, B.C., Gorai, A., "Fourth-Order Active Low Pass Filter for Biomedical Applications", *Journal of Mechanics of Continua and Mathematical Sciences*, Vol. 17, No. 8, pp. 12-18, August 2022.  
   [DOI: 10.26782/jmcms.2022.08.00002](https://doi.org/10.26782/jmcms.2022.08.00002)

2. Franco, S., *Design with Operational Amplifiers and Analog Integrated Circuits*, 4th Ed., McGraw-Hill Education.

3. Sallen, R.P. and Key, E.L., "A Practical Method of Designing RC Active Filters", *IRE Transactions on Circuit Theory*, Vol. 2, Issue 1, pp. 74-85, 1955.

4. Texas Instruments, *LMX24/LM2902 Op-Amp Datasheet and SPICE Model*, Texas Instruments Inc., 2024.

5. Texas Instruments, *Active Filter Design Techniques*, Op Amp Applications Handbook (SLOA049), Texas Instruments Inc., 2002.

6. FOSSEE Team, IIT Bombay, *eSim Research Migration Project*.  
   Available: [https://esim.fossee.in/research-migration-project](https://esim.fossee.in/research-migration-project)

## 🙏 Acknowledgments
- **FOSSEE, IIT Bombay** for the eSim Research Migration Project and promoting open-source EDA tools
- **Texas Instruments** for providing LM324 SPICE models
- **Department of Electronics & Communication Engineering, Jamia Millia Islamia** for academic support

## 📄 License
This project is open-source under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author
**Tooba Imtiyaz**  
Department of Electronics & Communication Engineering  
Faculty of Engineering & Technology  
Jamia Millia Islamia, New Delhi, India

## 📧 Contact
For questions or feedback, please open an issue on GitHub or contact the author.

---

**⭐ If you find this project useful, please give it a star!**

