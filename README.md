# Speech separation using Neural Networks
## Spectrogram_separation.py
This file uses two speech files as an input, combines them, and uses an Ideal Binary Mask to separate them again.
The two speech files are both padded with zeros to make them the same length, and further padded to pad the length to the nearest whole second. This was done to make implementing the STFT and iSTFT easier. 

![Alt text](SpeechSegregation/SpeechSegregationPictures/mixturesignals.png?raw=true "Mixture signals")

A STFT was then applied to the to the 2 speech signals and the mixture signal using a 0.05 second window.

![Alt text](SpeechSegregation/SpeechSegregationPictures/spectrograms.png?raw=true "Spectrograms")

A mask was then calculated using the SNR of the absolute value of the STFT of the clean signal of one of the speech signals divided by the absolute value of the STFT of the mixture signal. An IBM was created rounding this mask to the nearest integer and then applying a ceiling function so that any number greater than 1 was given the value 1.

![Alt text](SpeechSegregation/SpeechSegregationPictures/mask.png?raw=true "Mask")

The mixture signal is then combined with the mask using element-wise multiplication (Hadamard product). An iSTFT is then applied to the resulting array to obtain the original speech signal.

![Alt text](SpeechSegregation/SpeechSegregationPictures/recoverdsignal.png?raw=true "Recovered signal")

### Sources
http://scipy.github.io/devdocs/generated/scipy.signal.stft.html
http://www.cs.northwestern.edu/~pardo/courses/eecs352/lectures/MPM14-Time-Frequency-Masking.pdf

