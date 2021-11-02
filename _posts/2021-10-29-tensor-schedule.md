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

Auto-scheduler
------

TVM
======
TVM is a `Python` embedded language; its grammar is very much similar to `tensorflow`, `pytorch`.


AutoTVM
------
write some there