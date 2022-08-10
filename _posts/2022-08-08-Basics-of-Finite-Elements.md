---
title: "Basics of Finite Elements"
date: 2022-08-08
categories:
  - Blog
  - Research
tags:
  - FEM
  - Complex
---

<img src="/Users/longchen1/Dropbox/Math/MathNotes/camtips/assets/images/part1FEM2.png" alt="part1FEM2" style="zoom:80%;" />



What is finite element? From a function approximation point of view, a finite element space is a piecewise polynomial space defined on a grid. On the right is a surface defined on a square domain. The domain $\Omega$ is divided into small triangles, called a grid (mesh, or triangulation) $\mathcal{T}_{h}$, and the parameter $h$ represents the maximal diameter of small triangles. For each grid point, evaulate the function value, and then connect these point values with triangles in space, so that an approximation of the surface is obtained. All such piecewise linear polynomial and globally continuous functions constitute a linear finite element space.

This space is finite-dimensional, and its dimension is equal to the number of vertices of the mesh. The basis function corresponding to a vertex is drawn on the left. Because of its shape, we usually call it a hat function.

<img src="/Users/longchen1/Dropbox/Math/MathNotes/camtips/assets/images/part1FEM 5.png" alt="part1FEM 5" style="zoom:80%;" />

Let us now define finite elements mathematically. Ciarlet defines a finite element as a triple: $(K,V,\mathcal{N})$

-   $K$: element (triangle, square, tetrahedron, etc.)

-   $V$: shape function space (usually polynomial space $\mathbb{P}_{k}$)

-   $\mathcal{N}$: degrees of freedom (DoFs) ( a set of basis for the dual space $V’$)

**Unisolvence of Finite Elements**

For traditional finite elements, the shape function space is selected as a polynomial space, which is relatively easy. The key to constructing a finite element is to find a set of degrees of freedoms that satisfy

1.  It is a basis of dual space $V’$;

2.  The function defined has the desired continuity on the boundary.

To verify condition 1, the usual practice is divided into the following two steps:

-   1.1 **Count dimensions**. Verify that the number of degrees of freedom is equal to the dimension of the shape function space. One degree of freedom corresponds to one equation. The same number of dimensions means that the number of equations is equal to the number of unknowns. It looks very simple, isn't it just counting. Scalar functions are relatively simple, but when it comes to vector functions in high dimensions and high degrees, it is a bit difficult. When it comes to matrices or tensors, counting is not so simple. The reason is that these degrees of freedom are assigned to subsimplexes of different dimensions (vertices, edges, faces and volumes of tetrahedrons), and different components of vector and tensor functions are redistributed differently.

-   1.2 When the dimensions are the same, it is only necessary to prove that: for any function in the shape function space, if all the degrees of freedoms applied to this function are 0, then this function is 0. From the perspective of solving linear algebraic equations, if the right hand side is 0, then the solution can only be 0. To verify this step, generally recursively going from the vertex to the edge, then to the face, and finally to the volume, which requires characterization of the bubble functions, and the continuity to be described below is closely related.

To satisfy condition 2, that is, to satisfy the desired continuity, it is necessary to accurately characterize the trace of the corresponding Sobolev space. The finite element space is piecewise polynomials, but globally it belongs to a Sobolev space. The piecewise polynomials are glued together by the degrees of freedoms on the boundary of each element.

For a piecewise smooth function, it belongs to $H^{1}(\Omega)$, if and only if the function is globally continuous. In general, to be in $H^{m + 1}(\Omega)$, the function must belong $C^{m}(\Omega)$.

**Question:** Given a triangular mesh $\mathcal T_h$, construct piecewise polynomial and global $C^{m}(\Omega)$ finite element function space.

This problem is easy to solve in one dimension, and the resulting space is called a spline. The one-dimensional result can be extended to higher dimensions through tensor product grids. If it is a high-dimensional simplicial mesh, even a two-dimensional triangular mesh, the problem is not so simple. 

We will return to the construction of $C^{m}(\Omega)$ finite elements later on.

Let's go back and look at a few simple examples.

<img src="/Users/longchen1/Dropbox/Math/MathNotes/camtips/assets/images/part1FEM 6.png" alt="part1FEM 6" style="zoom:80%;" />

The shape function space is a linear (degree 1) polynomial $\mathbb{P}_{1}$. In $\mathbb R^2$, its dimension is 3, which can be determined by 3 degrees of freedoms. The DoFs of the element on the left are the values on the vertices, and the DoFs of the element on the right are the values on the midpoints of edges. Restricted to each triangle, both choices satisfy Condition 1, that is, a linear polynomial can be uniquely determined by either function values on 3 vertices or function values on 3 midpoints of edges.

The function on the left is continuous at the vertices of the triangle, and the function on the right is continuous at the midpoint of each edge. The left one is globally continuous and belongs to $H^{1}(\Omega)$, while the right one does not belong to $H^{1}(\Omega)$. So we call the left a $H^{1}$-conforming element, and the right one $H^{1}$-nonconforming element. According to the naming rules of discoverers, the left is called Lagrange element, and the right is called CR (Crouzeix–Raviart) element.

Non-conforming elements can also be used to solve PDEs, but the theoretical analysis is more complicated. In this series, we focus on conforming finite elements.

<img src="/Users/longchen1/Dropbox/Math/MathNotes/camtips/assets/images/part1FEM 7.png" alt="part1FEM 7" style="zoom:80%;" />

We then look at the quadratic element $\mathbb{P}_{2}$, whose dimension is 6. Then 6 DoFs are required. One option is 3 vertex values plus 3 edge midpoint values. This choice satisfies conditions 1 and 2. On the right is the basis function corresponding to vertex 1, which is a quadratic polynomial taking value 1 at point 1 and 0 at other points.

<img src="/Users/longchen1/Dropbox/Math/MathNotes/camtips/assets/images/part1FEM 8.png" alt="part1FEM 8" style="zoom:80%;" />There are other choices of 6 DoFs. If each edge is taken two points, the degrees of freedom formed in this way are not necessarily a basis of the dual space. That is, the DoFs chosen in this way are not necessarily linearly independent. If these 6 points are in a circle, the right hand side is a quadratic polynomial, which vanishes at the 6 points, but is non-zero itself.

Note that if these two points are taken as Gaussian quadrature points on the edge, it can ensure that the function is continuous across edges. That is, condition 2 can be satisfied, but condition 1 cannot. So it is not simply counting the dimensions.

This example was constructed by Fortin while trying to generalize CR linear non-conforming element to quadratic non-conforming element. High-order non-conforming elements are not easy to construct under the framework of finite elements, but can be better constructed under the framework of Weak Galerkin or Virtual Element spaces.

<img src="/Users/longchen1/Dropbox/Math/MathNotes/camtips/assets/images/part1FEM 9.png" alt="part1FEM 9" style="zoom:80%;" />

From $\mathbb P_1$ to $\mathbb P_2$ and to the higher order, the Lagrange element is easy to generalize to $\mathbb{P}_{k}$ for all integers $k\geq 1$. In two dimensions, the triangle is divided into four, and repeated $k-1$ times. The DoFs are the function values at the vertices of all small triangles.

**Exercise:** Prove that the unisolvence of DoFs and that the function defined is globally continuous.

<img src="/Users/longchen1/Dropbox/Math/MathNotes/camtips/assets/images/part1FEM 10.png" alt="part1FEM 10" style="zoom:80%;" />

The Lagrange element can also be easily extended to three dimensions. The idea is to divide the tetrahedron repeatedly, and then use the function values on vertices of the small tetrahedron as DoFs. The idea seems to be the same, but it's not so intuitive when it comes to 3D. A proof that seems obvious in 2D, is not so obvious in 3D, and such generalization is not trivial.

For example, consider a small problem first. In two dimensions, add the midpoints of the three edges, and then connect them to divide the triangle into four, and the four small triangles are similar. In three dimensions, add the midpoints of 6 edges, how to connect them to form small tetrahedrons, and how many small tetrahedrons are there? Are they similar? How to divide so that this process can be repeated, and the small tetrahedron formed will not degenerate.

From a programming point of view, the uniform refinement of 3D tetrahedral meshes is not so obvious, and requires strict rules on the order of vertices. For details, please refer to the `uniformrefine3` function in the ifem package.

> By the way, almost all figures are all produced using ifem. Welcome to download and try ifem.

**Exercise:** Prove the unisolvence of the three-dimensional Lagrange element and prove that the function defined is globally continuous.

After the 2D and 3D are done, what about the $n$-dimension? For a $n$-dimension simplex, add the midpoint of each edge, and then connect it into small simplexes, how many can it be divided into? After $k-1$ times  division, how many vertices are there in total? Is its number equal to the dimension of $\mathbb{P}_{k}(\mathbb{R}^{n})$? If it is equal, how to prove the unisolvence? How can we say that the function as a whole is continuous?

Interested readers can think about it, there is a very beautiful and complete answer to this question. We'll talk about it next time.
