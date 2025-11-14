<h1>Frequency Division Multiplexing</h1>

<h2>Aim:</h2>
To study and implement Frequency Division Multiplexing (FDM) and Demultiplexing using SCILAB by combining six different message signals into a single composite signal for transmission and then recovering each message signal at the receiver through demodulation and filtering.

<h2>Apparatus Required:</h2>
Computer system with SCILAB software installed.

<h2>Theory:</h2>
Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a unique carrier frequency. Each message is modulated with its respective carrier so that their frequency bands do not overlap. These modulated signals are then combined to form a single multiplexed signal for transmission. At the receiver end, the signal is demultiplexed by using the same carrier frequencies for demodulation, followed by low-pass filtering to recover the original baseband signals. FDM is widely used in radio broadcasting, cable television, and satellite communication systems where efficient bandwidth utilization is essential.

<h2>Algorithm:</h2>
1.Start the program and initialize the sampling frequency fs and time vector t.

2.Generate six message signals of different frequencies (150 Hz to 900 Hz) using sine functions.

3.Assign six distinct carrier frequencies (3 kHz to 13 kHz) to each message signal to avoid overlap.

4.Modulate each message signal by multiplying it with its corresponding carrier (Amplitude Modulation).

5.Add all modulated signals to obtain the combined FDM signal representing multiple channels.

6.Plot all six message signals and the multiplexed signal for observation.

7.Demodulate each signal by multiplying the FDM signal with its corresponding carrier frequency.

8.Apply a low-pass filter to extract the original baseband signals (recovering the messages).

9.Plot the demodulated signals to verify successful recovery.

10.End the program after confirming proper multiplexing and demultiplexing operation.

<h2>Code:</h2>

```

fs = 30000;
t = 0:1/fs:0.02;

fm = [150, 300, 450, 600, 750, 900];
m = [];

for i = 1:6
    m(i, :) = 4 * sin(2 * %pi * fm(i) * t);
end

fc = [3000, 5000, 7000, 9000, 11000, 13000];

fdm = zeros(1, length(t));
for i = 1:6
    c = cos(2 * %pi * fc(i) * t);
    s = m(i, :) .* c;
    fdm = fdm + s;
end

scf(1);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, m(i, :));
    title("Message Signal " + string(i));
end

scf(2);
clf;
plot(t, fdm);
title("Multiplexed FDM Signal");

demod = [];
for i = 1:6
    c = cos(2 * %pi * fc(i) * t);
    x = fdm .* c;
    h = ones(1, 200)/200;
    y = conv(x, h, 'same');
    demod(i, :) = y;
end

scf(3);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, demod(i, :));
    title("Recovered (Demodulated) Signal " + string(i));
end

```

<h2>Output Waveform</h2>

<img width="1579" height="988" alt="image" src="https://github.com/user-attachments/assets/2850a5e7-b52c-4613-8d98-9f4a21e61400" />

<img width="1605" height="894" alt="image" src="https://github.com/user-attachments/assets/8db52f75-6501-4d19-802d-47fdb674efa5" />

<img width="1580" height="974" alt="image" src="https://github.com/user-attachments/assets/d9e21d82-88a6-44ac-9a8d-7f381235c2e2" />


<h1>Result:</h1>

The Frequency Division Multiplexing (FDM) and Demultiplexing of six different message signals were successfully implemented using SCILAB.All six message signals were modulated with distinct carrier frequencies and combined to form a single multiplexed signal. Upon demodulation and low-pass filtering, each original message signal was accurately recovered, verifying the correct working of the FDM and demultiplexing process.
