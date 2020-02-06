The project end-goal is to be able to calculate the angle from Manta (AUV) to a sound source (pinger) under water. The pinger has a frequency range from 20-40kHz. To calculate the angle TDOA (Time Difference On Arrival) is used. The approach is to sample the sound with multiple hydrophones (microphones under water), and find the time difference on arrival. Using the differences it is possible to calculate both the angle and the distance. 

This program will focus on the angle. Three hydrophones is used to calculate the TDOA. The main problem is divided in to three main parts:
1. Hardware : Sampling the audio

2. DSP :Filtering out the noise and other frequencies, plus finding the TDOA with acceptable error.

3. Calculating the angle with the TDOA.

Hardware: STM32F767Zi is used to sample the audio. The microcontroller comes with 3x12 bits resolution ADC and DMA (Direct memory access), which is used to achieve a high-enough sampling frequency. Nyquist-theorem states that the sampling frequency must be 2 times the audio-frequency. The sampling frequency is currently 100kHz, but will probably be increased. 

DSP: A fourier transform is implemented to filter out non-wanted frequencies. Therefore, the main pingers frequency must be known beforehand. A FFT is only able to find frequencies equal to or less than the sampling frequency. To actually filter out the unwanted signals, their fourier coeffisients must be set to zero. Afterwards the code performs cross-correlation to fint the TDOA in the signals. 

Calculations: A space-geometric approach is used to find the angle.
(TODO picture and approach). The script can be found in "timediff.py". 

