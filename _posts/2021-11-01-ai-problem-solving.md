---
title: 'AI-Aided Problem Solving'
date: 2021-11-01
permalink: /posts/2021/11
tags:
  - Artificial Intelligence
  - Problem Solving
  - Problem Formulation
---

AI techniques/algorithms keep advancing these days, along with that  is an increasing interest on the question how these techniques and algorithms shall be harnessed for solving real-world problems.   In this blog, I provide some of my thoughts on problem-solving and artificial intelligence.

 

Traditional problem-solving
======

First, I would summarize traditional problem-solving using the following diagram. 

 ![traditional problem-solving](/images/traditional_solving.png)

Left is raw problem, say from industrial, that the problem-solver (e.g., an engineer or group of them) is trying to solve.   They would propose/design solutions, and these solutions are intrinsically related  to their understanding of the problem. They would then try to improve the solutions while observing the effect of these solutions. As their knowledge accumulate, a continual refinement of these solutions is expected.   

AI-aided problem-solving
======

![AI-aided problem-solving](/images/new_problem_solving.png)

I would capsulize the AI-aided problem-solving paradigm as above. Same as before, the problem-solver receives a raw-problem. 
The difference part is that problem-solver is now equipped extensive knowledge on AI --- these are useful in two aspects:    

- Problem Modelling
- Algorithm Development

While people usually pay a great attention on the aspect of **algorithm development**, in my opinion, the other aspect **problem modelling** is often overlooked.
The reason that I want to emphasize the role of problem modelling is simple: **algorithms for the raw-problem are built upon the surrogate formal problem model, so the capability of your algorithms would be limited by the restrictions emanated from the way the problem is formally defined --- on the other hand, a too general problem model would only create extra difficulty for the development of an algorithm specifically effective for the raw-problem you are interested.** 

Many sub-areas have seen relatively separate developments since the concept of [artificial intelligence](https://en.wikipedia.org/wiki/Dartmouth_workshop) beinging proposed. They are fundamentally motiviated by different [scientific inquiries](https://en.wikipedia.org/wiki/Models_of_scientific_inquiry). Some are motivated by the quest to understand the nature of knowledge, including how knowledge is represented, how they accumulate and how they reproduce each other.  
Some are more concerned about **learning**, while arguing that the knowledge might be more conveniently be considered as a fuzzy object (e.g., they might just be represented by a large set of floating numbers). Some are focused on the algorithmic procedures through which a well-defined goal can be achieved. 
In the above diagram I listed a few paradigms in AI that could either help *problem modelling* or *problem-solving*. 