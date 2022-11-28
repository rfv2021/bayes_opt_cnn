# Model Card

## Model Description
This convolutional neural network model classifies pictures of the cross-section of laser-written waveguides, in terms of the supported electromagnetic modes.

**Input:** 8-bit grayscale 32x32px images of the cross-section of waveguides;

**Output:** for each picture the model outputs a label which identifies the ([Hermite Gauss](https://en.wikipedia.org/wiki/Gaussian_beam)) electromagnetic modes supported by waveguide. The labels are (in order of complexity):

	- M=0 N=0 --> label 0
	- M=0 N=1 --> label 1
	- M=0 N=2 --> label 2
	- M=1 N=0 --> label 3
	- M=1 N=1 --> label 4
	- M=1 N=2 --> label 5
	- M=2 N=0 --> label 6
	- M=2 N=1 --> label 7
	- M=2 N=2 --> label 8

**Model Architecture:** Convolutional neural network with 2 convolutional layers and 3 fully connected layers. The model was fine tuned through bayesian optimisation to maximise the accuracy after 2 training epochs. The free parameters in the Bayesian optimisation were:

- The width of the convolution filters 1 and 2;
- The output depth of the convolution filter 1;
- The output depth of the convolution filter 2 ;
- Number of output features of fully connected layer 1;
- Number of output features of fully connected layer 2;
- The learning rate of the stochastic gradient descent optimiser;
- The momentum of the stochastic gradient descent optimiser.


## Performance
- The model performance was measured in terms of classification accuracy (acc) on an independent test set, containing 2 000 images. Several CNN configurations produce satisfying results. Around 30 configurations have acc > 95\%, after only 2 epochs of training. With 3 training epochs accuracies in excess of 99\% are found.
- For more details, see 3_Load Bayesian optimisation results.ipynb.

## Limitations
- The model was trained on waveguides conducting single modes and does not cover multi-modal operation, that is, it cannot classify waveguides which conduct several modes simultaneously.


## Trade-offs
- The model has not been evaluated with images from different cameras. This might deteriorate the performance and requires further study.