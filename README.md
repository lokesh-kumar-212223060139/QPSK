# QPSK
# Aim
Write a Python program for the modulation and demodulation of QPSK.
# Tools required
python 3.0
# Program

import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 100000  # Sampling frequency
fc = 20000   # Carrier frequency
bit_rate = 10000  # bits per second
samples_per_bit = fs // bit_rate
symbol_rate = bit_rate // 2
samples_per_symbol = fs // symbol_rate

# Generate random data (8 bits => 4 symbols)
data_bits = np.array([0,1, 1,0, 1,1, 0,0])  # Can be randomized

# Map bits to symbols (Gray coding: 00->0, 01->1, 11->2, 10->3)
bit_pairs = data_bits.reshape(-1, 2)
symbol_map = {
    (0, 0): (1, 1),
    (0, 1): (1, -1),
    (1, 1): (-1, -1),
    (1, 0): (-1, 1)
}
symbols = np.array([symbol_map[tuple(b)] for b in bit_pairs])

# Time vector
t = np.arange(0, len(symbols)*samples_per_symbol) / fs

# Generate I and Q components
I = np.repeat(symbols[:,0], samples_per_symbol)
Q = np.repeat(symbols[:,1], samples_per_symbol)

# Carrier waves
cos_wave = np.cos(2 * np.pi * fc * t)
sin_wave = np.sin(2 * np.pi * fc * t)

# Modulated signal
qpsk_signal = I * cos_wave + Q * sin_wave

# Plotting
plt.figure(figsize=(10, 8))

plt.subplot(4,1,1)
plt.plot(t, cos_wave)
plt.title('Unmodulated COSINE carrier wave')
plt.ylabel('amplitude')
plt.grid(True)

plt.subplot(4,1,2)
plt.plot(t, I)
plt.title('Waveform for in-phase component')
plt.ylabel('amplitude')
plt.grid(True)

plt.subplot(4,1,3)
plt.plot(t, Q)
plt.title('Waveform for quadrature component')
plt.ylabel('amplitude')
plt.grid(True)

plt.subplot(4,1,4)
plt.plot(t, qpsk_signal)
plt.title('Modulated QPSK signal')
plt.ylabel('amplitude')
plt.xlabel('time(sec)')
plt.grid(True)

plt.tight_layout()
plt.show()

# Output Waveform
![WhatsApp Image 2025-05-03 at 15 13 30_29653b9a](https://github.com/user-attachments/assets/b02de623-c157-487a-8356-b40e86f3421b)


# Results
thus Python program for the modulation and demodulation of QPSK verified
