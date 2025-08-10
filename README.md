# data-com

% Parameters
Fs = 10000;             % Sampling frequency (Hz)
t = 0:1/Fs:0.01;        % Time vector (10 ms)
fc = 1000;              % Carrier frequency (Hz)
fm = 100;               % Message frequency (Hz)
Am = 1;                 % Message amplitude
Ac = 1;                 % Carrier amplitude
kf = 2 * pi * 75;       % Frequency sensitivity (rad/s per unit amplitude)

% Message signal
m = Am * cos(2 * pi * fm * t);

% Integrate the message signal
int_m = cumsum(m) / Fs;

% FM signal
s_fm = Ac * cos(2 * pi * fc * t + kf * int_m);

% Plotting
figure;

subplot(3,1,1);
plot(t, m);
title('Message Signal');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(3,1,2);
plot(t, cos(2*pi*fc*t));
title('Carrier Signal');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(3,1,3);
plot(t, s_fm);
title('FM Signal');
xlabel('Time (s)');
ylabel('Amplitude');
