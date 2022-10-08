---
title: 'Some thought on AlphaTensor'
date: 2022-10-08
permalink: /posts/2022/10/
tags:
  - AlphaTensor
  - matrix multiplication
---

Recently, there is a heated attention on newly released paper [AlphaTensor](https://www.nature.com/articles/s41586-022-05172-4)  from DeepMind.
The claim in the **Abstract** seems to imply that there is a great advancement for a 50 year old problem that [Strassen's algorithm](https://en.wikipedia.org/wiki/Strassen_algorithm) was trying to address. This is really an intriguing claim, thus I spared myself some time trying to fully understand to what extent these claims are true, and how the algorithm they use looks like for such achievements. 

My personal thoughts are as follows.

Overall: 
1.  In terms of the results, it seems to me some "claims" are a bit exaggerated.  
AlphaTensor did update the state-of-the-art on some cases for matrix multiplication. 
However, it also seems to me that these cases are all from scenarios where few people have devoted their effort on.  The emphasis on the advancement of a 50-year old problem seems a little misleading, the problem better solved by AlphaTensor is not really the same problem Strassen was solving 50 years ago.  

2.  In terms of the algorithm. This is more interesting, although the article only emphasizes the [AlphaZero](https://en.wikipedia.org/wiki/AlphaZero) was used.  After having a deeper look, what I see is that it differs from `AlphaZero` in a number of places: 
   - the search space modeling: **extensive domain knowledge** are used for constructing the search space, e.g. for action pruning, equivalence mapping, state transformation and featurization; (this seems to be like a striking contradiction to the **Zero knowledge** aspect of `AlphaZero`).  
   - MCTS algorithm: one major new component is the use of sampling to build the search tree;
   - a mixture of supervised learning and reinforcement learning.


Further comments on the results: 

1) The result on the *4x4* matrix. This result is highlighted in Abstract, which shows that 4x4 might be a case of great interest to domain experts. The article says that from Strassen’s 49 times multiplication, AlphaTensor reduced it to 47 times.  But after a careful reading, I realized that this is not a result on a "real matrix", but a finite filed, i.e., modular arithmetic {0, 1}.  I believe that many people might wonder the same as me: **how important is 4x4 {0, 1} modular matrix multiplication in practice?**

2) The result of 4x5, 5x5 matrix multiplication. This result is indeed obtained on the real numbers. The best solution is 80 multiplications, and AlphaTensor pushed it to 76 times.  This looks like a more impressive result, but it was not highlighted in Abstract.  **It seems that irregular cases like 4x5, 5x5 are those few people would pay attention, maybe have smaller practical value?**

3) The result of 3x3. AphaTensor obtained the result of 23 multiplications, which is not emphasized in this paper, probably because the result has been published in other papers last year.  That paper uses the "SAT modeling + pure search" solution, which was applied only for 3x3 matrix. It seems that the  SAT SAT would become unmanageably large for 4x4 or larger matrices. However, I have not yet checked the technical details of this solution. Just wondering **if more research effort and computation resources are used in this line of development, would it achieve same or better results than AlphaTensor?**

4) GPU/TPU Runtime results.  The paper did not seem to put much emphasis on results from this part.  It is just trying to show that, if the optimization objective of AlphaTensor is modified to reduce real-hardware runtime, by deploying AlphaTensor upon GPU/TPU compiler (e.g. XLA), they can achieve about 20% improvement.  It should be emphasized that best matrix multiplication found for GPU  is not TPU friendly, and vice versa. This is more reasonable, since in practice, best runtime when the hardware architecture is best exploitation for computation & data reuse, yet GPU and TPU differs significantly in architecture design.  The “runtime” objective does not match the “Strassen objective”, either. As mentioned in the paper, the solution found by AlphaTensor  does not contain less multiplication arithmetic than Strassen’s algorithm. It is just more suited for TPU/GPU.  Since the only modification that they did is changing the reward function, I suspect that **if more adjustments are posed to the AlphaZero algorithm itself for the runtime objective, better results/improvements might be achieved.** 


