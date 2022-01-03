---
title: "Simplicial Lattice and Lagrange Elements"
date: 2022-01-02
categories:
  - Blog
tags:
  - Research
  - FEM
---



We use Lagrange elements as an example to introduce the simplicial lattice and construction of finite elements based on a decomposition of the simplicial lattice. Brief explanation will be given after some slides. Proofs included in the slides are short and less rigorous. The readers are encouraged to read the reference for all details.

**Reference**: [Geometric decompositions of the simplicial lattice and smooth finite elements in arbitrary dimension](https://arxiv.org/abs/2111.10712) Long Chen and Xuehai Huang. *arXiv.* 2021.



![geoLa 29](https://lyc102.github.io/camtips/assets/images/geoLa 29.png)

![geoLa 30](https://lyc102.github.io/camtips/assets/images/geoLa 30.png)

The DoFs are not just functional defined on the shape function $V$​. Indeed it is implicitly assumed a DoF $N(u)$​ can be extended to function $u$​ in a larger space $U$​ so that $V\subset U$​​. 

![geoLa 31](https://lyc102.github.io/camtips/assets/images/geoLa 31.png)

![geoLa 32](https://lyc102.github.io/camtips/assets/images/geoLa 32.png)

Let's look at two examples. The shape function is now the quadratic polynomial whose dimension is $6$​​​. Function values at $3$​​ vertices and middle points of $3$​​ edges are well defined DoFs. But $6$​ points sitting on the same circle are not as a qudratic polynomial can vanish at those $6$​​ points only. This is the example found by Fortin when he wants to generalize the linear CR non-conforming element to quadratic. 



Let's do that.
