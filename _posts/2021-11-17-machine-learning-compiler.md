---
title: 'Deep Learning Frameworks and Compilers'
date: 2021-11-17
permalink: /posts/2021/Nov-17
tags:
  - tensor programs
  - compiler 
---

In previous blogs, we have covered the topic of **scheduling tensor programs**. 
This task might be viewed as one step in **machine learning compilers**, 
which I will provide an introduction in this blog.


Compilers are inherently designed to abridge the gap between **software** and **hardware**. 
In the same sense, **machine learning compilers** are primarily developed for hardware for machine learning programs, e.g., deep neural networks. 

AI accelerators
======

Due to the successes of deep neural networks and other machine learning applications, specific hardware devicies have been developed for these computer programs. 
These hardware might be collectively referred to as **AI accelerators**, as their major aim is to *accelerate* tensor program computations. 

In below I list some chips that might be used for AI computation: 

- CPUs -- this is the most generic chips we see everday, and of course, they are able to execute tensor programs though it has high latency.   
- NVIDIA GPUs, e.g., microarchitectures [Volta, 2017](https://en.wikipedia.org/wiki/Volta_(microarchitecture)), [Turing, 2018](https://en.wikipedia.org/wiki/Turing_(microarchitecture)), and [Ampere, 2020](https://en.wikipedia.org/wiki/Ampere_(microarchitecture))
- Google's [TPUs](https://en.wikipedia.org/wiki/Tensor_Processing_Unit). So far, four versions have been released, i.e., TPU-v1 in 2016, TPU-v2 in 2017, TPU-v3 in 2018, and TPU-v4 in 2021. [An Edge TPU is announced in 2018, and has been used in Pixel-4 smart phone](https://en.wikipedia.org/wiki/Tensor_Processing_Unit#cite_note-34).
- [Huawei's Ascend Series](https://pdfs.semanticscholar.org/4ca3/69ee20343433bd50c288c01ebcba2d6a03b2.pdf).
  See paper ([Ascend: a Scalable and Unified Architecture for Ubiquitous Deep Neural Network Computing : Industry Track Paper](https://ieeexplore.ieee.org/document/9407221))
  ![Ascend series](/images/Ascend_series.png "Ascend series, figure from Liao et al.")
- Others: they are many [other AI accelerators](https://en.wikipedia.org/wiki/Deep_learning_processor).


Tensor programs software frameworks (neural net frameworks)
=======
Having only a dedicated hardware is insufficient to accelerating tensor program computations. 
They need also software support. Over the past few years, many neural network frameworks have been developed. 
To name a few, [Tensorflow](https://tensorflow.org), [Pytorch](https://pytorch.org), [JAX](https://github.com/google/jax), and Huawei's [Mindspore](https://github.com/mindspore-ai/mindspore).

<!---
![DL software stack](/images/dl_software_stack.png "DL sofware stack")
--->
<p align="center">
    <img src="/images/dl_software_stack.png" title="DL sofware stack, figure from Liao et al.">
</p>

These frameworks are all created under the above software architecture stack, among which the core question being addressed is **how to translate high-level and hardware-agnostic code into low-level, efficient and hardware-aware code**. 
In fact, this *core task* is fairly identical despite how different these software frameworks may look in appearance. 
Thus, deep learning compilers do have the right of being exist as standalone projects. Some of them are listed in below.

Machine compilers 
======
This specifically refers to the "intermidiate" part of the software framework above. 

1. XLA
------
[XLA](https://www.tensorflow.org/xla), developed by Google, originally for tensorflow, but now also supports *Pytorch*, *JAX*.

2. GLOW
------
[GLOW](https://github.com/pytorch/glow), developed by Facebook. 

3. Tiramisu
------
[Tiramisu](http://tiramisu-compiler.org/), developed by MIT.

4. TensorComprehensions
------
[TensorComprehensions](https://github.com/facebookresearch/TensorComprehensions) by Facebook.

5. AutoTVM
------
[AutoTVM](https://tvm.apache.org/docs/reference/api/python/autotvm.html), as the name indicates, is developed in TVM, but it supports also many other front-ends, e.g. *Tensorflow*, *Pytorch* etc. 

6. Halide
------
[Halide](https://halide-lang.org) is a language in `C++` as well as a compiler. 
It was first created for accelerating image processing pipelines, but can also be used for deep neural network models, given that
the model specification has been converted into Halide's `C++` language. 

Difference Summary
-------
In summary, the differences of these tools are majorly reflected in the following aspects:

- frontend language expressiveness. For example, Halide does not support cyclic computation graphs, e.g., LSTMs. 

- search space modelling. For example, *Tiramisu* models the scheduling space using `Polyhedral`, while Halide models the search space as a 
  decision tree.

- algorithms for scheduling. For example, *Tiramisu* uses ILP solver. AutoTVM used evolutionary algorithms. Halide uses tree search.

- backend support

MLIR
=======
Besides the algorithmic differences, all the tools above rely certain format of **intermidate representation**, 
which is usually developed for that specific tool.  It would ideal that design on this aspect can be standardized, thus different 
*compilers* can mostly focus on developing intelligent compilation algorithms, rather than engineering seemingly different but in-theory equivalent designs.
The [MLIR](https://mlir.llvm.org/) represnets an effort towards unifying these intermediate representations.

![ML compiler](/images/ml_compiler_MLIR.png "intelligent compiler")