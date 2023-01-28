# Lab 1

## Lab 1 Exercise 1
![l1e1](./images/GetImage.png)

This is the result of "HOT NAME" by inputting my full name into the system. My name is a "COLD Name" 

I also try to figure the HOTNAME output from this system. __It seems like only if the name containing all "Z" will output HOT.__ 

## Lab 1 Exercise 2 

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

 ## LAB 1 Exercise 3 

In this exercise, we are going to build an AM modulator and graph the output of the modulated signals. The equation for modulating a single tone signal is given by: 
 
![l1e3](./images/19.PNG)

__Question 1:__ Adjust plots using graph tools and show the block diagram: 

![l1e3q11](./images/GetImage%20(7).png)

As shown in the diagram above, the two graphs in the first row represent the message signal with a frequency of 1000Hz and the frequency diagram that shows the message signal's frequency.  

The graphs in the second row show the modulated signals (carrier and message signal) and the frequency diagram of the modulated signal. 

![l1e3q12](./images/GetImage%20(8).png)


This is the block diagram of how we design it. 

 

>Notice: What is a PSD block? 

>A Power Spectral Density (PSD) is the measure of signal's power content versus frequency. A PSD is typically used to characterize broadband random signals. PSD is a tool similar to Fast Fourier Transform (FTT). The PSD and FFT are both tools for measuring and analyzing a signal's frequency content. The FFT transfers time data to the frequency domain, which allows engineers to view changes in frequency values. The PSD takes another step and calculates the power, or strength, of the frequency content. 

__Question 2:__ Set 𝐴𝑐 = 2 and change 𝐴𝑚 in the panel window to obtain the modulation index values 𝜇 = {0.5,1, 1.5}. For each value of 𝜇 plot the time domain and PSD representations of both the message and modulated signals. What is the impact of the modulation index on the modulated signal? Explain your answer. 
 
![l1e3q21](./images/GetImage%20(9).png)


Modulation index (μ) = 0.5 

The signal is under-modulated signal. This can create the original cosine signal with the right frequency. 

![l1e3q22](./images/GetImage%20(10).png)

Modulation index (μ) = 1 

The signal is a perfect-modulated signal. The modulated signal perfectly represents a cosine signal with frequency of 1kHz. 

![l1e3q23](./images/GetImage%20(11).png)

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