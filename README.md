# selection

## Installation

This software is written in C++ and requires the GNU scientific library to run. Download all the files and compile with

```
g++ -O3 -lgsl *.cpp -o sr
```

## Generating allele frequency bridges

To generate a bridge, following the logic of Schraiber et al (2013), use the flag -b, followed by a comma separated list,
`x0,xt,gamma,t`, i.e. the initial frequency, the final frequency, the selection coefficient, and the timespan of the bridge.

For example,

```
./sr -b 0.2,0.6,100,0.2 > myTraj.txt
```

will output a trajectory for an allele with gamma = 100 going from a frequency of 0.2 to 0.6 in 0.2 diffusion time units into the file myTraj.txt. Trajectory files consist of two lines, the first being the allele frequency trajecotry and the second line being the time points.

## Inference from allele frequency time series

The basic input for generating an inference of selection coefficients and allele ages from an allele frequency time series are

1. Sampling times, in units of 2N_0 generations
2. Sample sizes, in number of chromosomes
3. Counts of the derived allele, in number of chromsoomes
4. A population size history

It's very important that you are consistent in setting the time scale between items 1 and 4. 

The population size history is a 3-column white-space-separated file. Each line is one epoch of population size, which can be constant or exponential growth. For each epoch, each column is

1. The population size at the most *ancient* time in the epoch, relative to N_0
2. The growth rate of that epoch, scaled by 2N_0
3. The most ancient time of the epoch, in units of 2N_0 generations

The repository includes two sample population size histories, `constant.pop`, which reflects a constant population size, and `horse.all.pop`, which reflects the population history of horses as described by Der Sarkissian et al (2015).

## Other flags that might be relevant

```
-d maximum spacing between time points
-g minimum number of time points
-t number of tests to calibrate rejection sampling algorithm
-e random number seed
```
