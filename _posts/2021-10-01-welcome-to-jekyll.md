---
title: "Welcome to Jekyll"
date: 2021-10-01
categories:
  - Blog
tags:
  - Tag1
  - Mathematics
  - iFEM
---


## Code

```matlab
totalEdge = uint32(sort([elem(:,[2,3]); elem(:,[3,1]); elem(:,[1,2])],2));
[edge,i2,j] = myunique(totalEdge);
NT = size(elem,1);
elem2edge = uint32(reshape(j,NT,3));
i1(j(3*NT:-1:1)) = 3*NT:-1:1; 
i1 = i1';
k1 = ceil(i1/NT); 
k2 = ceil(i2/NT); 
t1 = i1 - NT*(k1-1);
t2 = i2 - NT*(k2-1);
ix = (i1 ~= i2); 
neighbor = uint32(accumarray([[t1(ix),k1(ix)];[t2,k2]],[t2(ix);t1],[NT 3]));
edge2elem = uint32([t1,t2,k1,k2]);
```

## LaTeX

Equation
$$E = mc^2,
\tag{1}$$

Multiline equation
$$
\displaystyle
\int_{\Omega}  \nabla \boldsymbol{\phi} : \nabla\boldsymbol{\psi} = 
\int_{\Omega}\Big( (\nabla\times \boldsymbol{\phi}) \cdot (\nabla\times \boldsymbol{\psi}) + (\nabla 
\cdot 
\boldsymbol{\phi}) (\nabla \cdot \boldsymbol{\psi}) \Big)
\\
\displaystyle
\quad + \int_{\partial \Omega} 
\Big( \underbrace{\nabla_{\Gamma}(\boldsymbol{n}\cdot \boldsymbol{\phi}_n)\cdot 
\boldsymbol{\psi}_{\Gamma}}_{\text{tangential}} - 
\underbrace{(\nabla\cdot\boldsymbol{\phi}_{\Gamma})(\boldsymbol{n}\cdot\boldsymbol{\psi}_{n})}_{\text{normal}}
\Big).
\tag{$\ast$}
\label{eq:multi}
$$

Refering equation: \eqref{eq:multi}.

