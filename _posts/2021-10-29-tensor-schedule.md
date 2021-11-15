---
title: 'Scheduling tensor programs'
date: 2021-10-29
permalink: /posts/2021/10/
tags:
  - tensor programs and neural nets
  - compiler optimization
  - machine learning
---

Tensor programs are ubiquitous, ranging from [general matrix muliplication](#) to [deep neural networks](#). However, due to extensive float number computation, execution them can incur high **latency**. Indeed, it is well-known that the rejuvenation of neural networks is very much due 
to the use of *GPUs* for these computation --- thus accelerating tensor programs is of great importance. 

The remaining question is *how should we achieve that*? In below I capsulize the methods into two categories: 

1. Optimize the tensor program with either **reformulation** or **approximation**
  - Reformulation: this optimizes only the algorithm from which the tensor program is created. For example, 
  [Strassen's algorithm](https://en.wikipedia.org/wiki/Strassen_algorithm) accelerates matrix multiplication since it uses less multiplications.
  - Approximation: this kind of opitmization generates a new tensor program that is similar but is "cheaper". For example, by [quantization](https://towardsdatascience.com/how-to-accelerate-and-compress-neural-networks-with-quantization-edfbbabb6af7), one can obtain a significantly smaller network whose peformance is usually similar to the original net.

2. Optimize the execution with hardware advancement
  - This keeps tensor program untouched, but instead optimzing how they could be executed on a given hardware. For example, the development of [cuDNN](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjWs9q8nPjzAhW-JTQIHf-zCooQFnoECAwQAQ&url=https%3A%2F%2Farxiv.org%2Fabs%2F1410.0759&usg=AOvVaw1FnAFnzSHX1By7EEN4wFSg) is one such endeavour.

We are primarily interested in category 2), but with yet one more aspiration: **automate the process.** 
The approach to this end requires two ingredients: 

- A language --- this refers to a domain specific language through which tensor program can be specified. 
- A compiler --- this refers to a tool that can translate the high-level source code into **efficient** low-level implementation.

In below are two instances of the above idea.

Halide
======
Halide is a `C++` embedded language, proposed [Jonathan Ragan-Kelley](#) and [Andrew Adams](#) in 2012.

Auto-schedulers
------

- [OpenTuner: An extensible framework for program autotuning](#) 

  By Jason Ansel et al., PACI 2014

- [Automatically Scheduling Halide Image Pipelines](#)

  By Mullapudi et al. SIGGRAPH 2016

- [Differentiable Programming for Image Processing and Deep Learning in Halide](#)

  By Tzu-Mao Li eta al., SIGGRAPH 2018
  
- [Learning to Optimize Halide with Tree Search and Random Programs](https://halide-lang.org/papers/autoscheduler2019.html)

  By Andrew Adams et al., SIGGRAPH 2019 

- [Efficient automatic scheduling of imaging and vision pipelines for the GPU](https://dl.acm.org/doi/abs/10.1145/3485486)

  By Lunke Andreson et al., Proceedings of the ACM on Programming Languages 2021

TVM
======
TVM is a `Python` embedded language; its grammar is very much similar to `tensorflow`, `pytorch`.


Auto-schedulers
------
- AutoTVM:

  [Learning to Optimize Tensor Programs](https://dl.acm.org/doi/pdf/10.5555/3327144.3327258)

  By Chen et al., Neurips 2018   

- Ansor: 

  [Ansor : Generating High-Performance Tensor Programs for Deep Learning](https://www.usenix.org/conference/osdi20/presentation/zheng)

  By Zhang et al., USENIX 2020


Difference between Halide and TVM
======

Language expressiveness difference
------
Halide supports `DAG` like computational logics. 
TVM is fully compatible with `Tensorflow` and `PyTorch`, so it also supports recurrent network architectures.

Auto-scheduler algorithms difference
------
- The autoscheduler in Halide schedules a program `stage by stage`, where a `stage` is a functional object. At each stage, it makes two type of decisions
    - Cross-stage granularity: 
    - Intra-stage order:  

- The autoscheduler in TVM divides the computation graph into independent `operators` (an operator is similar to a stage in Halide), then optimize each operator separately. 
