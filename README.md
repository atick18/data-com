# data-com

% Parameters
Fs = 10000;             
t = 0:1/Fs:0.01;       
fc = 1000;             
fm = 100;              
Am = 1;                 
Ac = 1;                
kf = 2 * pi * 75;      

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



clc;
clear;
f = 5;                 
fs = 100;              
t = 0:1/fs:1;          
x = sin(2*pi*f*t);      

% Quantization
n_bits = 2;                     
L = 2^n_bits;                   
x_min = min(x); x_max = max(x);
q_step = (x_max - x_min) / (L - 1);   

% Uniform quantizer
xq_index = round((x - x_min) / q_step);    
xq = xq_index * q_step + x_min;            


bin_pcm = dec2bin(xq_index, n_bits);       

figure;
plot(t, x, 'b', 'LineWidth', 1.5);
hold on;
stairs(t, xq, 'r', 'LineWidth', 1.5);
xlabel('Time (s)');
ylabel('Amplitude');
title('PCM Encoding of a Sine Wave');
legend('Original Signal', 'Quantized Signal');
grid on;
