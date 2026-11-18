<div align="center">

# 📡 5G / 6G Communication Lab

### ECA5603 · Experiment Records & Assignments

![Experiments](https://img.shields.io/badge/Experiments-15-blue?style=for-the-badge) ![Outputs](https://img.shields.io/badge/Outputs-35-success?style=for-the-badge) ![Code files](https://img.shields.io/badge/Code%20files-13-purple?style=for-the-badge) ![Assignments](https://img.shields.io/badge/Assignments-4-orange?style=for-the-badge)

*Code, output screenshots and reports for the ECA5603 5G/6G lab, organised and numbered in order.*

</div>

---

## 📑 Quick Jump

| | | | | | |
|---|---|---|---|---|---|
| [Exp01](#exp01) | [Exp02](#exp02) | [Exp03](#exp03) | [Exp05](#exp05) | [Exp06](#exp06) | [Exp07](#exp07) |
| [Exp09](#exp09) | [Exp10](#exp10) | [Exp11](#exp11) | [Exp13](#exp13) | [Exp14](#exp14) | [Exp15](#exp15) |
| [Exp17](#exp17) | [Exp18](#exp18) | [Exp19](#exp19) | [Assignments](#assignments) |  |  |

## 🗂️ Folder Structure

```text
ExpNN/
└── A/ B/ C/ D/             one folder per part
    ├── ExpNN_A.png         output screenshot
    └── ExpNN_A_code.txt    code (where available)
Assignments/            reports and assignment files
```

> Experiment numbers that are missing (4, 8, 12, 16) are not in the repo yet.

---

## 🧪 Experiments

> Click an experiment to expand its outputs and code.

<a id="exp01"></a>
<details>
<summary><b>Experiment 01</b> &nbsp;·&nbsp; 4 parts</summary>


#### Part A

<img src="Exp01/A/Exp01_A.png" width="560" alt="Exp01_A.png">

<details>
<summary>📄 Code · <a href="Exp01/A/Exp01_A_code.txt">Exp01_A_code.txt</a></summary>

```
clear;
clc;
close all;

% System parameters
totalBandwidthHz = 1e6;
fdmaChannelHz = 200e3;
tdmaSlots = 8;
processingGain = 64;
targetSIRdB = 7;

% Calculate user capacity
fdmaUsers = floor(totalBandwidthHz / fdmaChannelHz);
tdmaUsers = tdmaSlots;

targetSIR = 10^(targetSIRdB / 10);
cdmaUsers = floor(1 + processingGain / targetSIR);

% Capacity values
method = {'FDMA', 'TDMA', 'CDMA'};
users = [fdmaUsers, tdmaUsers, cdmaUsers];

% Plot graph
figure;
bar(users);

set(gca, 'XTick', 1:3, 'XTickLabel', method);

xlabel('Multiple Access Technique');
ylabel('Maximum Supported Users');
title('FDMA, TDMA and CDMA Capacity Comparison');

grid on;
```

</details>


#### Part B

<img src="Exp01/B/Exp01_B.png" width="560" alt="Exp01_B.png">

<details>
<summary>📄 Code · <a href="Exp01/B/Exp01_B_code.txt">Exp01_B_code.txt</a></summary>

```
clear;
clc;
close all;

% System parameters
processingGain = 64;
targetSIRdB = 7;

% Number of simultaneous users
K = 2:30;

% Calculate SIR
sirLinear = processingGain ./ (K - 1);
sirDb = 10 * log10(sirLinear);

% Plot graph
figure;
plot(K, sirDb, 'bo-', 'LineWidth', 1.5);

hold on;
yline(targetSIRdB, 'r--', 'Target SIR');

xlabel('Number of Simultaneous CDMA Users (K)');
ylabel('Estimated SIR (dB)');
title('CDMA SIR versus Number of Users');

legend('Estimated SIR', 'Target SIR');
grid on;

hold off;
```

</details>


#### Part C

<img src="Exp01/C/Exp01_C.png" width="560" alt="Exp01_C.png">

<details>
<summary>📄 Code · <a href="Exp01/C/Exp01_C_code.txt">Exp01_C_code.txt</a></summary>

```
clear;
clc;
close all;

figure;
hold on;

colors = lines(4);

for u = 1:4
    rectangle('Position', [0, u-1, 1, 0.8], ...
        'FaceColor', colors(u,:), ...
        'EdgeColor', 'k');

    text(0.5, u-0.6, sprintf('User %d', u), ...
        'HorizontalAlignment', 'center');
end

xlim([0 1]);
ylim([0 4]);

xlabel('Time');
ylabel('Frequency Channel');
title('FDMA Resource Allocation');

set(gca, 'YTick', []);
grid on;

hold off;
```

</details>


#### Part D

<img src="Exp01/D/Exp01_D.png" width="560" alt="Exp01_D.png">

<details>
<summary>📄 Code · <a href="Exp01/D/Exp01_D_code.txt">Exp01_D_code.txt</a></summary>

```
% OBJECTIVE 4: RESOURCE-ALLOCATION DIAGRAMS

clear;
clc;
close all;

% Create figure with three diagrams
figure;
tiledlayout(1, 3);

% Colors for four users
colors = lines(4);

%% FDMA: Different frequency channels

nexttile;
hold on;

for u = 1:4
    rectangle('Position', [0, u-1, 1, 0.8], ...
        'FaceColor', colors(u,:), ...
        'EdgeColor', 'k');

    text(0.5, u-0.6, sprintf('User %d', u), ...
        'HorizontalAlignment', 'center');
end

xlim([0 1]);
ylim([0 4]);

xlabel('Time');
ylabel('Frequency Channel');
title('FDMA');

set(gca, 'YTick', []);
hold off;


%% TDMA: Different time slots

nexttile;
hold on;

for u = 1:4
    rectangle('Position', [u-1, 0, 0.8, 1], ...
        'FaceColor', colors(u,:), ...
        'EdgeColor', 'k');

    text(u-0.6, 0.5, sprintf('User %d', u), ...
        'HorizontalAlignment', 'center');
end

xlim([0 4]);
ylim([0 1]);

xlabel('Time Slot');
ylabel('Frequency Channel');
title('TDMA');

set(gca, 'YTick', []);
hold off;


%% CDMA: Shared frequency band with different codes

nexttile;
hold on;

for u = 1:4
    rectangle('Position', [0, 0, 1, 1], ...
        'FaceColor', colors(u,:), ...
        'FaceAlpha', 0.22, ...
        'EdgeColor', colors(u,:), ...
        'LineWidth', 1.5);
end

text(0.5, 0.62, 'Users 1-4 share', ...
    'HorizontalAlignment', 'center');

text(0.5, 0.40, 'band; different codes', ...
    'HorizontalAlignment', 'center');

xlim([0 1]);
ylim([0 1]);

xlabel('Time');
ylabel('Frequency Band');
title('CDMA');

set(gca, 'YTick', []);
hold off;

% Overall title
sgtitle('FDMA, TDMA and CDMA Resource Allocation');
```

</details>

</details>

<a id="exp02"></a>
<details>
<summary><b>Experiment 02</b> &nbsp;·&nbsp; 3 parts</summary>


#### Part A

<img src="Exp02/A/Exp02_A.jpeg" width="560" alt="Exp02_A.jpeg">


#### Part B

<img src="Exp02/B/Exp02_B.jpeg" width="560" alt="Exp02_B.jpeg">


#### Part C

<img src="Exp02/C/Exp02_C.jpeg" width="560" alt="Exp02_C.jpeg">

</details>

<a id="exp03"></a>
<details>
<summary><b>Experiment 03</b> &nbsp;·&nbsp; 2 parts</summary>


#### Part A

<img src="Exp03/A/Exp03_A.jpeg" width="560" alt="Exp03_A.jpeg">


#### Part B

<img src="Exp03/B/Exp03_B.jpeg" width="560" alt="Exp03_B.jpeg">

</details>

<a id="exp05"></a>
<details>
<summary><b>Experiment 05</b> &nbsp;·&nbsp; 3 parts</summary>


#### Part A

<img src="Exp05/A/Exp05_A.png" width="560" alt="Exp05_A.png">

<details>
<summary>📄 Code · <a href="Exp05/A/Exp05_A_code.txt">Exp05_A_code.txt</a></summary>

```
clc;
clear;
close all;

% Parameters
BW1 = 20;          % Component carrier bandwidth (MHz)
SE = 4;            % Spectral efficiency (bits/s/Hz)
Ncc = 1;           % Number of component carriers

% Calculations
BWagg = BW1 * Ncc;
Throughput = BWagg * SE;   % Throughput in Mbps

% Display Results
disp('Single Component Carrier');
disp(['Bandwidth = ', num2str(BWagg), ' MHz']);
disp(['Estimated Throughput = ', num2str(Throughput), ' Mbps']);

% Plot Graph
figure;
bar(Ncc, Throughput);

grid on;
xlabel('Number of Component Carriers');
ylabel('Estimated Throughput (Mbps)');
title('LTE-Advanced Single Carrier Throughput');
```

</details>


#### Part B

<img src="Exp05/B/Exp05_B.png" width="560" alt="Exp05_B.png">

<details>
<summary>📄 Code · <a href="Exp05/B/Exp05_B_code.txt">Exp05_B_code.txt</a></summary>

```
clc;
clear;
close all;

% Parameters
BWcc = 20;                  % Bandwidth per component carrier (MHz)
SE = 4;                     % Spectral efficiency (bits/s/Hz)
CC = [1 2 3];               % Number of component carriers

% Calculations
AggBW = BWcc .* CC;         % Aggregated bandwidth (MHz)
Throughput = AggBW .* SE;   % Estimated throughput (Mbps)

% Display Results
disp('CC   Aggregated BW (MHz)   Estimated Throughput (Mbps)');
disp([CC' AggBW' Throughput']);

% Plot Graph
figure;
bar(CC, Throughput);

grid on;
xlabel('Number of Aggregated Component Carriers');
ylabel('Estimated Throughput (Mbps)');
title('LTE-Advanced Carrier Aggregation Throughput');
```

</details>


#### Part C

<img src="Exp05/C/Exp05_C.png" width="560" alt="Exp05_C.png">

<details>
<summary>📄 Code · <a href="Exp05/C/Exp05_C_code.txt">Exp05_C_code.txt</a></summary>

```
clc;
clear;
close all;

% Parameters
BW = [5 10 15 20];       % Carrier bandwidths (MHz)
SE = 4;                  % Spectral efficiency (bits/s/Hz)

% Throughput Calculation
TP = BW .* SE;           % Estimated throughput (Mbps)

% Display Results
disp('Bandwidth (MHz)   Throughput (Mbps)');
disp([BW' TP']);

% Plot Graph
figure;
plot(BW, TP, 'o-', 'LineWidth', 2);

grid on;
xlabel('Carrier Bandwidth (MHz)');
ylabel('Estimated Throughput (Mbps)');
title('Throughput vs Component Carrier Bandwidth');
```

</details>

</details>

<a id="exp06"></a>
<details>
<summary><b>Experiment 06</b> &nbsp;·&nbsp; 3 parts</summary>


#### Part A

<img src="Exp06/A/Exp06_A.png" width="560" alt="Exp06_A.png">

<details>
<summary>📄 Code · <a href="Exp06/A/Exp06_A_code.txt">Exp06_A_code.txt</a></summary>

```
clc;
clear;
close all;

% SNR Range
SNR_dB = 0:2:20;

% Initialize BER Arrays
BER_SISO = zeros(size(SNR_dB));
BER_MIMO = zeros(size(SNR_dB));

% Simulation Loop
for k = 1:length(SNR_dB)

    N = 10000;

    % Generate Random Bits
    bits = randi([0 1], N, 1);

    % BPSK Modulation
    tx = 2 * bits - 1;

    % Convert SNR from dB to Linear
    snrLin = 10^(SNR_dB(k)/10);

    % SISO Channel Simulation
    noise = randn(N, 1) / sqrt(2 * snrLin);
    rx = tx + noise;

    bits_hat = real(rx) > 0;

    BER_SISO(k) = mean(bits_hat ~= bits);

    % Simple 2x2 MIMO Equivalent Link
    H = (randn(2,2) + 1j * randn(2,2)) / sqrt(2);

    h_eff = sqrt(sum(abs(H(:)).^2) / 2);

    noise2 = randn(N, 1) / sqrt(2 * snrLin);

    rx2 = h_eff * tx + noise2;

    bits_hat2 = real(rx2) > 0;

    BER_MIMO(k) = mean(bits_hat2 ~= bits);

end

% Plot BER Performance
figure;

semilogy(SNR_dB, BER_SISO, 'o-', 'LineWidth', 2);
hold on;

semilogy(SNR_dB, BER_MIMO, 's-', 'LineWidth', 2);

grid on;

xlabel('SNR (dB)');
ylabel('Bit Error Rate (BER)');

title('SISO and MIMO BER Performance');

legend('SISO', 'MIMO');
```

</details>


#### Part B

<img src="Exp06/B/Exp06_B.png" width="560" alt="Exp06_B.png">

<details>
<summary>📄 Code · <a href="Exp06/B/Exp06_B_code.txt">Exp06_B_code.txt</a></summary>

```
% BER and Reliability Analysis

clc;
clear;
close all;

% SNR Range
SNR_dB = 0:2:20;

% Initialize Reliability Array
Reliability = zeros(size(SNR_dB));

% Simulation Loop
for k = 1:length(SNR_dB)

    N = 10000;

    % Generate Random Bits
    bits = randi([0 1], N, 1);

    % BPSK Modulation
    tx = 2 * bits - 1;

    % Convert SNR from dB to Linear
    snrLin = 10^(SNR_dB(k)/10);

    % Add Gaussian Noise
    noise = randn(N, 1) / sqrt(2 * snrLin);

    % Received Signal
    rx = tx + noise;

    % Demodulation
    bhat = real(rx) > 0;

    % Calculate Bit Error Rate
    BER = mean(bhat ~= bits);

    % Calculate Reliability
    Reliability(k) = 1 - BER;

end

% Plot Reliability Graph
figure;

plot(SNR_dB, Reliability, 'o-', 'LineWidth', 2);

grid on;

xlabel('SNR (dB)');
ylabel('Reliability (1-BER)');

title('Communication Reliability vs SNR');
```

</details>


#### Part C

<img src="Exp06/C/Exp06_C.png" width="560" alt="Exp06_C.png">

<details>
<summary>📄 Code · <a href="Exp06/C/Exp06_C_code.txt">Exp06_C_code.txt</a></summary>

```
clc;
clear;
close all;

% Parameters
N = 8;                              % Number of antenna elements
theta = -90:1:90;                   % Observation angle
steer = [-60 -30 0 30 60];          % Steering directions

% Initialize Gain Array
gain = zeros(size(steer));

% Beamforming Gain Calculation
for k = 1:length(steer)

    % Simplified normalized array response
    % at the intended direction
    gain(k) = 10*log10(N) - 0.01*abs(steer(k));

end

% Plot Beamforming Gain
figure;

plot(steer, gain, 'o-', 'LineWidth', 2);

grid on;

xlabel('Steering Angle (Degrees)');
ylabel('Beamforming Gain (dB)');

title('Beamforming Gain for Different Steering Directions');
```

</details>

</details>

<a id="exp07"></a>
<details>
<summary><b>Experiment 07</b> &nbsp;·&nbsp; 3 parts</summary>


#### Part A

<img src="Exp07/A/Exp07_A.png" width="560" alt="Exp07_A.png">

<details>
<summary>📄 Code · <a href="Exp07/A/Exp07_A_code.txt">Exp07_A_code.txt</a></summary>

```
clc;
clear;
close all;

% Parameters
Nsc = 24;                    % Number of subcarriers
Nsym = 14;                   % OFDM symbols per slot

% Initialize Resource Grid
grid = zeros(Nsym, Nsc);

% Simplified Downlink (DL) Assignment
grid(1:10, :) = 1;

% Simplified Uplink (UL) Assignment
grid(11:14, :) = 2;

% Plot Resource Grid
figure;

imagesc(grid);

grid on;

xlabel('Subcarrier Index');
ylabel('OFDM Symbol Index');

title('Simplified 5G NR Time-Frequency Resource Grid');

colorbar;
```

</details>


#### Part B

<img src="Exp07/B/Exp07_B.png" width="560" alt="Exp07_B.png">

<details>
<summary>📄 Code · <a href="Exp07/B/Exp07_B_code.txt">Exp07_B_code.txt</a></summary>

```
clc;
clear;
close all;

% 5G NR Numerology Parameters
scs = [15 30 60 120 240];       % Subcarrier spacing (kHz)
mu = 0:4;                      % Numerology index
slot = [1 0.5 0.25 0.125 0.0625]; % Slot duration (ms)

% Plot 1: Subcarrier Spacing vs Slot Duration
figure;

plot(scs, slot, 'o-', 'LineWidth', 2);

grid on;

xlabel('Subcarrier Spacing (kHz)');
ylabel('Slot Duration (ms)');

title('5G NR Slot Duration for Different Subcarrier Spacing');

% Plot 2: Numerology vs Subcarrier Spacing
figure;

bar(mu, scs);

grid on;

set(gca, 'XTick', mu);

xlabel('Numerology Index (\mu)');
ylabel('Subcarrier Spacing (kHz)');

title('5G NR Subcarrier Spacing for Different Numerologies');
```

</details>


#### Part C

<img src="Exp07/C/Exp07_C.png" width="560" alt="Exp07_C.png">

<details>
<summary>📄 Code · <a href="Exp07/C/Exp07_C_code.txt">Exp07_C_code.txt</a></summary>

```
clc;
clear;
close all;

% OFDM Symbol Index
symbols = 1:14;

% Downlink and Uplink Allocation
DL = [1 1 1 1 1 1 1 1 1 1 0 0 0 0];

UL = [0 0 0 0 0 0 0 0 0 0 1 1 1 1];

% Plot Downlink and Uplink Assignment
figure;

plot(symbols, DL, 'o-', 'LineWidth', 2);
hold on;

plot(symbols, UL, 's-', 'LineWidth', 2);

grid on;

xlabel('OFDM Symbol Index');
ylabel('Allocation Status');

title('Simplified Downlink and Uplink Assignment');

legend('Downlink', 'Uplink');
```

</details>

</details>

<a id="exp09"></a>
<details>
<summary><b>Experiment 09</b> &nbsp;·&nbsp; 1 part</summary>


#### Part A

<img src="Exp09/A/Exp09_A.png" width="560" alt="Exp09_A.png">

</details>

<a id="exp10"></a>
<details>
<summary><b>Experiment 10</b> &nbsp;·&nbsp; 1 part</summary>


#### Part A

<img src="Exp10/A/Exp10_A.png" width="560" alt="Exp10_A.png">

</details>

<a id="exp11"></a>
<details>
<summary><b>Experiment 11</b> &nbsp;·&nbsp; 1 part</summary>


#### Part A

<img src="Exp11/A/Exp11_A.png" width="560" alt="Exp11_A.png">

</details>

<a id="exp13"></a>
<details>
<summary><b>Experiment 13</b> &nbsp;·&nbsp; 1 part</summary>


#### Part A

<img src="Exp13/A/Exp13_A.png" width="560" alt="Exp13_A.png">

</details>

<a id="exp14"></a>
<details>
<summary><b>Experiment 14</b> &nbsp;·&nbsp; 1 part</summary>


#### Part A

<img src="Exp14/A/Exp14_A.png" width="560" alt="Exp14_A.png">

</details>

<a id="exp15"></a>
<details>
<summary><b>Experiment 15</b> &nbsp;·&nbsp; 4 parts</summary>


#### Part A

<img src="Exp15/A/Exp15_A.png" width="560" alt="Exp15_A.png">


#### Part B

<img src="Exp15/B/Exp15_B.png" width="560" alt="Exp15_B.png">


#### Part C

<img src="Exp15/C/Exp15_C.png" width="560" alt="Exp15_C.png">


#### Part D

<img src="Exp15/D/Exp15_D.png" width="560" alt="Exp15_D.png">

</details>

<a id="exp17"></a>
<details>
<summary><b>Experiment 17</b> &nbsp;·&nbsp; 3 parts</summary>


#### Part A

<img src="Exp17/A/Exp17_A.png" width="560" alt="Exp17_A.png">


#### Part B

<img src="Exp17/B/Exp17_B.png" width="560" alt="Exp17_B.png">


#### Part C

<img src="Exp17/C/Exp17_C.png" width="560" alt="Exp17_C.png">

</details>

<a id="exp18"></a>
<details>
<summary><b>Experiment 18</b> &nbsp;·&nbsp; 2 parts</summary>


#### Part A

<img src="Exp18/A/Exp18_A.png" width="560" alt="Exp18_A.png">


#### Part B

<img src="Exp18/B/Exp18_B.png" width="560" alt="Exp18_B.png">

</details>

<a id="exp19"></a>
<details>
<summary><b>Experiment 19</b> &nbsp;·&nbsp; 3 parts</summary>


#### Part A

<img src="Exp19/A/Exp19_A.png" width="560" alt="Exp19_A.png">


#### Part B

<img src="Exp19/B/Exp19_B.png" width="560" alt="Exp19_B.png">


#### Part C

<img src="Exp19/C/Exp19_C.png" width="560" alt="Exp19_C.png">

</details>

---

<a id="assignments"></a>
## 📚 Assignments

| File | |
|---|---|
| Assignment_4.pdf | [Open](Assignments/Assignment_4.pdf) |
| ECA56_CO1_Ratish_Harikrishna(192512414).docx | [Open](Assignments/ECA56_CO1_Ratish_Harikrishna(192512414).docx) |
| ECA56_CO2_Assignment2_Report.docx | [Open](Assignments/ECA56_CO2_Assignment2_Report.docx) |
| ECA56_CO3_Design_Report.docx | [Open](Assignments/ECA56_CO3_Design_Report.docx) |

---

<div align="center">

⭐ *ECA5603 · 5G/6G Lab Record*

</div>
