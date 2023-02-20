<div id="top"/>

# Communication Lab

Steven Shao, 27/01/2023

* [Lab 1 Exercise 1](#lab1e1)
* [Lab 1 Exercise 2](#lab1e2)
* [Lab 1 Exercise 3](#lab1e3)
* [Lab 2 Exercise 1](#lab2e1)
* [Lab 2 Exercise 2](#lab2e2)
* [Lab 2 Exercise 3](#lab2e3)
* [Lab 2 Exercise 4](#lab2e4)

<div id="lab1e1"/>

# Lab 1
## Lab 1 Exercise 1
![l1e1](./images/GetImage.png)

This is the result of "HOT NAME" by inputting my full name into the system. My name is a "COLD Name" 

I also try to figure the HOTNAME output from this system. __It seems like only if the name containing all "Z" will output HOT.__ 

<div id="lab1e2"/>

### [Lab 1 Exercise 2](#top)

__Question 1:__ Include the block diagram and the front panel in your logbook.  

![l1e2q11](./images/GetImage%20(1).png)
![l1e2q12](./images/GetImage%20(2).png)

__Question 2:__ Create a control for stopping the execution of the program after 1000 iterations. Set the value of “number of bins” to 10. Include the corresponding histogram in your logbook.  
![l1e2q21](./images/GetImage%20(3).png)

Here I add an Equal logic to compare "I" value with 1000 to be the end condition. 

![l1e2q22](./images/GetImage%20(4).png)

The output from this system have a normal distribution with mean of 5 and a small standard deviation. In the next task, we are going to change it into standard normal distribution. 
 
__Question 3:__ Revise your code such that the final distribution you observe in the histogram is a standard Normal distribution (i.e., it has zero mean and unit variance). Include the revised block diagram in your logbook, and explain each of the changes you have made. 

![l1e2q31](./images/GetImage%20(5).png)

Inside LABVIEW, there is a "statistic block" under the diagram tab. This block can output the value of expectation, variance, and standard deviation of a signal based on the input signal. The equation of transforming a normal distribution into a standard normal one is by subtracting expectation and divide by the standard deviation. Therefore, I connect the output signal from the Add Array Elements function into the Statistic Block, do the operation, and feed the signal back into the Histogram Function. The output below is indeed a standard normal distribution. 

![l1e2q32](./images/GetImage%20(6).png)

<div id="lab1e3"/>

 ### [LAB 1 Exercise 3](#top)

In this exercise, we are going to build an AM modulator and graph the output of the modulated signals. The equation for modulating a single tone signal is given by: 
 
![l1e3](./images/19.PNG)

__Question 1:__ Adjust plots using graph tools and show the block diagram: 

![l1e3q11](./images/GetImage%20(7).png)

As shown in the diagram above, the two graphs in the first row represent the message signal with a frequency of 1000Hz and the frequency diagram that shows the message signal's frequency.  

The graphs in the second row show the modulated signals (carrier and message signal) and the frequency diagram of the modulated signal. 

![l1e3q12](./images/1.jpg)


This is the block diagram of how we design it. 

 

>Notice: What is a PSD block? 

>A Power Spectral Density (PSD) is the measure of signal's power content versus frequency. A PSD is typically used to characterize broadband random signals. PSD is a tool similar to Fast Fourier Transform (FTT). The PSD and FFT are both tools for measuring and analyzing a signal's frequency content. The FFT transfers time data to the frequency domain, which allows engineers to view changes in frequency values. The PSD takes another step and calculates the power, or strength, of the frequency content. 

__Question 2:__ Set 𝐴𝑐 = 2 and change 𝐴𝑚 in the panel window to obtain the modulation index values 𝜇 = {0.5,1, 1.5}. For each value of 𝜇 plot the time domain and PSD representations of both the message and modulated signals. What is the impact of the modulation index on the modulated signal? Explain your answer. 
 
![l1e3q21](./images/2.jpg)


Modulation index (μ) = 0.5 

The signal is under-modulated signal. This can create the original cosine signal with the right frequency. 

![l1e3q22](./images/3.jpg)

Modulation index (μ) = 1 

The signal is a perfect-modulated signal. The modulated signal perfectly represents a cosine signal with frequency of 1kHz. 

![l1e3q23](./images/4.jpg)

Modulation index (μ) = 1.5 

The signal is an over-modulated signal, where the signal is distorted and can no longer represent the original cosine signal. 

### __*Background Information:*__

The modulation index is often denoted in percentage called as Percentage of Modulation. We will get the percentage of modulation, just by multiplying the modulation index value with 100. For a perfect modulation, the value of modulation index should be 1, which implies the percentage of modulation should be 100%. 

For instance, if this value is less than 1, i.e., the modulation index is 0.5, then the modulated output would look like the following figure. It is called as Under-modulation. Such a wave is called as an under-modulated wave. 

![l1e3q24](./images/GetImage.jpeg)


If the value of the modulation index is greater than 1, i.e., 1.5 or so, then the wave will be an over-modulated wave. It would look like the following figure. 

![l1e3q25](./images/GetImage%20(1).jpeg)


Over-Modulated signals are undesirable, because the modulated signals got distorted. The carrier signal experiences a 180 degree phase reversal, which causes additional sidebands. The resulting demodulated signal can no longer represents the original signal. 

__Question 3:__ Set 𝐴𝑐 = 1 and 𝐴𝑚 = 1. Change the frequency of the message signal to 𝑓𝑚 = {1𝑘, 2𝑘, 5𝑘}. What is the impact of the varying frequency value on the modulated signal? Explain your answer.  

![l1e3q31](./images/GetImage%20(12).png)

fm = 1k 

![l1e3q32](./images/GetImage%20(13).png)

fm = 2k 

![l1e3q33](./images/GetImage%20(14).png)

fm = 5k 

The varying message frequency changes the modulated signal's frequency graph. The cosine wave's frequency modulation graph is creating to spikes around the carrier frequency (plus or minus the message frequency). When frequency increases, the separation between the spikes increases. 

 
In the last step, we created a sub-VI for this design, similar to a sub-module. 

![l1e3q34](./images/GetImage%20(15).png)

<div id="lab2e1"/>

# Lab 2 AM Simulation and USRP

### [Lab 2 Exercise 1](#top)
In this task, we are going to demodulate the amplitude modulated signal using two method. 

1. Coherent demodulation: multiply AM signal with carrier signal and apply a low pass filter.
2. Envelope Detection: Rectify AM signal, low pass filtered, and remove DC component.

#### Exercise 1a (Coherent):
This is the block diagram of the model:
![l2p1](./images/l2p1.jpg)
![l2p3](./images/l2p3.jpg)

* In the diagram, we can remove the DC component by applying `Amplitude Measurements` module. We can input the signal, and the module can output the DC value. Remeber to use `single shot` mode.
* `Filter` module can create a low pass filter

The original signal is given by:

![l2e3](./images/19.PNG)

By multiplying the carrier signal and applying a low pass filter, we can get the following result:

![l2p6](./images/l2p6.jpg)

The output from the low pass filter is a combination of a DC value and the message signal, so we have to minus the DC value to recover the true message signal. Setting Ac = 2 to adjust the constant.


#### Exercise 1b (Envelope):
Block Diagram:
![l2p2](./images/l2p2.jpg)
![l2p4](./images/l2p4.jpg)

* Multiplication of $\Pi$ is used to amplify the signal and compensate the loss from rectification.

> Rectifier does not have a simple impulse response, a diode that performs  rectification is a non-linear component and thus does not have a linear impulse response. But when we rectify a periodic signal, its impulse response looks like a square wave with same period T. (All negative value = 0). The convolution of cosine message signal with square wave has the following frequency response. At low frequecny, amplutude = 1/$\Pi$ with A = 1/2, so a multiplication of $\Pi$ is needed before rectification.

![l2p7](./images/l2p7.jpg)

* `Waveform Properties` and `Build Waveform` are dual blocks. The first one decompose a waveform into complex array, while the second one reconstruct the wave from from data array. In this design, we decompose the signal, set negative values to zero, and reconstruct to achieve rectification.


__*How Envelope Detection works:*__

The diode detector acts like a rectifier that cuts of any negative compenent. The red line is the envelope, which in this case is the message signal. After passing through the low pass filter and minus the DC value, the only thing remaining is the red line (message signal) centered around DC.

![l2p8](./images/l2p8.jpg)

<div id="lab2e2"/>

### [Lab 2 Exercise 2: AM Simulation](#top)
Block diagram:

![l2p5](./images/l2p5.jpg)

After setting the variables to the correct value and changing the message signal amplitude from 1 to 4, we observed that the coherent method is receiving the exact same signal while the envelop detection method failed to function after message amplitude is greater than 2. Instead, the second method received distorted signal.

Message amplitude = 1:

![l2p9](./images/l2p9.jpg)

Message amplitude = 2:

![l2p10](./images/l2p10.jpg)

Message amplitude = 3:

![l2p11](./images/l2p11.jpg)

Message amplitude = 4:

![l2p12](./images/l2p12.jpg)

This distortion comes from the mathematical logic behind the method. Remember, the AM signal has the equation:

![l2e3](./images/19.PNG)

The envelope detection line received the signal `Ac + Amcos(2pifmt)`. If Ac > Am/under modulation, the system is fine, becuase all the message signal is fully on the upper half plane. 

![l2p13](./images/l2p13.jpg)

However, if Ac < Am / overmodulated, the amplitude of the carrier is already fliped, so we cannot recover the original message signal

![l2p14](./images/l2p14.jpg)

<div id="lab2e3"/>

### [Lab2 Exercise 3](#top)
niUSRP is a communication module that can send and receive signals.
Several components explanation:

![l2p15](./images/l2p15.jpg)

![l2p16](./images/l2p16.jpg)

![l2p17](./images/l2p17.jpg)

Transimitter side:

![l2p18](./images/l2p18.jpg)

Recevier side:

![l2p19](./images/l2p19.jpg)

#### Task 2:
Transmit a single-tone message signal with frequency 5kHz and modulation index 1:

![l2p20](./images/l2p20.jpg)

The signal is perfectlly received at the receiver side, with PSD showing a high peak at 5000 HZ.

#### Task 3: Observing noise:
Gain at receiver end is set to 20dB.

Modulation index = 0.8:

![l2p21](./images/l2p21.jpg)

Modulation index = 0.7:

![l2p22](./images/l2p22.jpg)

Modulation index = 0.6:

![l2p23](./images/l2p23.jpg)

Modulation index = 0.5:

![l2p24](./images/l2p24.jpg)

At this modulation index, noises started to appear on both frequency and time domain.

<div id="lab2e4"/>


### [Lab2 Exercise 4: Listerning to AM Music](#top)
When running `USRP_AM_Rx_Music.gvi`, the music is received after around 1 minutes, because IQ rate is 100k, very high.

> Not sure why IQ rate/sampling frequency affect time of receiving signal

![l2p25](./images/l2p25.jpg)

> video: music recorded


