Part 4: Thermal Noise Simulation & AnalysisObjective: To simulate and analyze thermal (Johnson-Nyquist) noise using MATLAB and visualize its characteristics in both the time and frequency domains.1. MATLAB ImplementationThe following code generates a thermal noise signal based on the parameters: $B=1$ MHz, $R=100$ $\Omega$, and $T=300$ K.Matlab% Parameters
B = 1e6;            % Bandwidth (1 MHz)
R = 100;            % Resistance (100 Ohms)
T = 300;            % Temperature (300 Kelvin)
k = 1.38e-23;       % Boltzmann constant
n_samples = 10000;  % Number of samples

% Time vector
time = 0 : 1/B : (n_samples-1) / B;

% Generate Thermal Noise (V_rms = sqrt(4kTRB))
thermal_noise = sqrt(4 * k * T * R * B) * randn(1, n_samples);

% --- Plotting Time Domain ---
figure;
subplot(2,1,1);
plot(time, thermal_noise);
title('Thermal Noise - Time Domain');
xlabel('Time (s)');
ylabel('Voltage (V)');
grid on;

% --- Power Spectral Density (PSD) Analysis ---
[psd, freq] = pwelch(thermal_noise, [], [], [], B);
subplot(2,1,2);
semilogx(freq, 10*log10(psd));
title('Power Spectral Density (PSD)');
xlabel('Frequency (Hz)');
ylabel('Power/Frequency (dB/Hz)');
grid on;
2. Observations & AnalysisFeatureObservationTime Domain VariationThe noise amplitude fluctuates randomly around zero. Because it is generated using randn, it follows a Gaussian (Normal) distribution, which is characteristic of thermal noise.Frequency DistributionThe PSD plot appears relatively "flat" across the spectrum. This confirms that thermal noise is White Noise, meaning its power is distributed equally across all frequencies within the simulated bandwidth.Parameter ImpactIncreasing Temperature (T) or Resistance (R) directly increases the variance (power) of the noise, resulting in higher amplitude spikes in the time domain and a higher baseline in the PSD plot.
