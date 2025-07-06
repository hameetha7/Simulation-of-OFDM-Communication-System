# 📶 Simulation of OFDM Communication System using MATLAB

This project demonstrates the simulation of a complete **Orthogonal Frequency Division Multiplexing (OFDM)** system using MATLAB. It provides insights into the design, transmission, and performance evaluation of modern wireless communication systems, such as LTE, Wi-Fi, and 5G.

---

## 🎯 Objective

To implement a MATLAB-based simulation of an OFDM communication system and analyze its performance by:
- Simulating modulation/demodulation
- Adding channel noise (AWGN)
- Calculating **Bit Error Rate (BER)** vs **Signal-to-Noise Ratio (SNR)**

---

## 🛠️ Tools & Technologies

- MATLAB (R2020 or later)
- Signal Processing Toolbox (optional)
- Concepts used:
  - QPSK / BPSK Modulation
  - IFFT / FFT for OFDM
  - AWGN channel modeling
  - BER computation

---

## ⚙️ System Workflow

1. **Bit Stream Generation** – Generate random bits to transmit  
2. **Modulation** – Map bits to symbols using BPSK/QPSK  
3. **OFDM Modulation** – Use IFFT to generate time-domain signal  
4. **Channel Simulation** – Add noise using AWGN  
5. **OFDM Demodulation** – Use FFT to recover frequency-domain data  
6. **Demodulation** – Convert symbols back to bits  
7. **BER Calculation** – Compare transmitted vs received bits

---

## 🖥️ Sample Code Snippet

```matlab
N = 64; % Number of subcarriers
numSymbols = 1000;
data = randi([0 1], N*numSymbols, 1);

modData = pskmod(data, 2); % BPSK
modData = reshape(modData, N, numSymbols);

ifftData = ifft(modData); % OFDM modulation

% Add noise
snr = 10;
rxSignal = awgn(ifftData, snr, 'measured');

% OFDM demodulation
fftData = fft(rxSignal);
rxData = reshape(fftData, [], 1);
rxBits = pskdemod(rxData, 2);

% BER
[numErr, ber] = biterr(data, rxBits);
fprintf("BER at SNR=%d dB: %f\n", snr, ber);
