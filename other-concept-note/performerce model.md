# performerce model

roofline model

![image-20241207150353146](C:\Users\86138\AppData\Roaming\Typora\typora-user-images\image-20241207150353146.png)

## Empirical Roofline Toolkit (ERT) for machine characterization

the peak compute performance (FLOP/s) and peak bandwidth

## Arithmetic Intensity (AI) and achieved performance (FLOP/s)

run time, total number of FLOPs performed, and the total number of bytes moved (both read and written)

[Nsight Compute](https://docs.nvidia.com/nsight-compute/2020.1/ProfilingGuide/index.html#roofline)

 We will focus on the NVIDIA V100 GPU architecture, and the tools discussed will be [nvprof](https://docs.nvidia.com/cuda/profiler-users-guide/index.html) and [Nsight Compute](https://docs.nvidia.com/nsight-compute/NsightCompute/index.html).

[the Roofline on NVIDIA GPUs repository](https://gitlab.com/NERSC/roofline-on-nvidia-gpus).

### Arithmetic Intensity

 the ratio of total floating-point operations (FLOPs) 

## Application Performance