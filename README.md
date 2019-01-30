# Benchmark for running a script that uses deep convolutional network

## Motivation
When I first started playing with machine learning,  I didn't have a machine with the GPU that can accelerate training.
However, as I got more serious, I noticed that it takes too much time to train on CPU and bought Nvidia GeForce GTX 1050 Ti for my Linux desktop. 
card.  As I got even more serious, I upgraded GPU to GeForce GTX 1080.  Ever since then, when I write ML code on my Mac mini, I almost always run on my Linux desktop.  I really haven't measured how much faster the GPU is as I know that it's just too slow to run my job on CPU.  However, I realized that it would be nice if I can say how much faster in a concrete term instead
of saying "Much faster."  So I decided to run a benchmark test using the modified version of my CIFAR-10 script.

# Results
I ran the script 3 times on each machine and documented the result in below tables.
For each script execution, a function to train the model is called 4 times.
In terms of the wall-clock time, for each script run, the third and fourth call to train the model seem to provide stabilized number.
Namely, for Mac, results in seconds are:
28.086050, 28.610886, 28.562303, 28.036568, 28.602799, 28.396387 with the mean 28.382499.

For Linux,
0.178514, 0.177793, 0.177940, 0.177911, 0.178042, 0.178016 with the mean 0.178036


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


