# Benchmark for running a script that uses deep convolutional neural network
January 30, 2019
&nbsp;
Hide Inada
## Motivation
When I first started playing with machine learning,  I didn't have a machine with a GPU that can accelerate training.
However, as I got more serious about AI, I noticed that it was taking too long to train on my Mac mini. I bought a Nvidia GeForce GTX 1050 Ti for my Linux desktop to speed up my experiment.
As I got even more serious, I upgraded the GPU to GeForce GTX 1080.  Ever since then, when I write ML code on my Mac mini, I almost always run my experiment on my Linux desktop.  I really haven't measured how much faster training on a GPU is as opposed to a CPU.  That's because I already know that it's just too slow to run my job on CPU.  However, I realized that it would be nice if I can say how much faster in a concrete term instead of saying "Much faster."  So I decided to run a benchmark test using [a modified version of my CIFAR-10 script](https://github.com/hideyukiinada/cifar10/blob/master/project/keras_25).

# Results
I ran the script 3 times on each machine and documented the result in tables at the end of this article.
For each script execution, a function to train the model is called 4 times.  For each call, time to complete the call was logged.  So overall elapsed time was measured 12 times.

In terms of wall-clock time, for each script run, the third and fourth calls to train the model seem to provide consistent numbers.
Namely, for Mac, results in seconds are:
28.086050, 28.610886, 28.562303, 28.036568, 28.602799, 28.396387 with the mean 28.382499.

For Linux, equivalent results are:
0.178514, 0.177793, 0.177940, 0.177911, 0.178042, 0.178016 with the mean 0.178036

If I divide 28.382499 by 0.178036, I'd get 159.419999325979

So, for this training, **Linux with the 1080 GPU was 159x faster than the Mac mini with CPU**.
When I was running my scripts to test accuracy against CIFAR-10, it took 5+ hours to run 100 epochs (e.g. 5.17 hours for the keras_29 script).  If I had run these scripts on my Mac mini, it would have taken 795 hours or 33 days.  I haven't seen a performance metrics between the latest version of Macbook Pro vs 2014 Mac mini, but I doubt that it's 159x faster.

## Implications
I'd like to share my view on how the need for GPU would impact software development companies who are or will be building a team of ML developers or data scientists for image processing (classification/object detection/generation) using a convolutional neural network.  My experience is more limited for NLP, but my experience is that LSTM is also slow to train on CPU which is demonstrated by the fact that there is a special Keras LSTM class for GPU called [CuDNNLSTM](https://keras.io/layers/recurrent/).
Because of the slowness of training on CPU, a developer in the above mentioned ML areas, GPU is not a nice to have hardware, but a must-have as it is nearly impossible for a developer to develop an ML application and wait for 30+ days to get a result of a single run.

I see two paths forward.  One is to use a crowd vendor's GPU environment such as AWS.  Another option is to work with the IT team for getting a desktop with an highend GPU.  The first option may be relatively painless if your CI and production environment already run in crowd vendor's space.  However, if you have a inhouse CI environment, that means that you also need to have the CI environment set up with the crowd vendor to do an official training of a model and test.
If you go for the second option, then instead of or in addition to handing out a high-end laptop, you also need to start handing out a desktop or a special laptop with a high-end GPU.  Also, before you buy a GPU, you may want to research to see what GPU cards are compliant with Nvidia's licensing terms. For example, this article from a year ago discusses [the prohibition of a GeForce card](https://www.theregister.co.uk/2018/01/03/nvidia_server_gpus/).

## Script used
[Modified version of CIFAR-10 classification script](https://github.com/hideyukiinada/benchmark/blob/master/project/benchmark1) to just run a single batch

## Machines used
* Home-built Linux desktop (OS: Ubuntu 18.10, RAM: 48 GB, CPU: 3.4 GHz Intel Core i5-7500, GPU: NVIDIA GeForce GTX 1080, Python: 3.6.7, TensorFlow-GPU: 1.12.0, Keras: 2.2.4)
* Mac mini (Late 2014) (OS:10.13.5, RAM: 16 GB, CPU: 2.6 GHz Intel Core i5, Python: 3.6.7, TensorFlow: 1.12.0, Keras: 2.2.4)

## Complete Results

### Result on Mac #1

| # | Process time | Wall time |
|---|---|---|
|1 | 103.070201 | 54.792648 |
|2 | 76.877656 | 28.602382 |
|3 | 76.605735 | 28.086050 |
|4 | 77.116006 | 28.610886 |

### Result on Mac #2

| # | Process time | Wall time |
|---|---|---|
|1 | 104.752804 | 56.123174 |
|2 | 78.961987 | 30.115714 |
|3 | 76.096431 | 28.562303 |
|4 | 77.223991 | 28.036568 |

### Result on Mac #3

| # | Process time | Wall time |
|---|---|---|
|1 | 101.952952 | 53.308898 |
|2 | 76.955266 | 27.672237 |
|3 | 76.044292 | 28.602799 |
|4 | 76.837717 | 28.396387 |

### Result on Linux #1

| # | Process time | Wall time |
|---|---|---|
|1 | 15.410076 | 15.327186 |
|2 | 0.215100 | 0.204940 |
|3 | 0.178330 | 0.178514 |
|4 | 0.182779 | 0.177793 |

### Result on Linux #2

| # | Process time | Wall time |
|---|---|---|
|1 | 15.399605 | 15.316593 |
|2 | 0.183949 | 0.178353 |
|3 | 0.182133 | 0.177940 |
|4 | 0.183427 | 0.177911 |

### Result on Linux #3

| # | Process time | Wall time |
|---|---|---|
|1 | 15.461966 | 15.384140 |
|2 | 0.184064 | 0.178244 |
|3 | 0.182690 | 0.178042 |
|4 | 0.182478 | 0.178016 |


