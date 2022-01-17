---
title: Matrices
---

# Matrices
 
> Most of the material in this section was borrowed from [this excellent series of Essence of Linear Algebra youtube videos](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) 

## Linear Transformation

![linear-combination](images/linear-combination.png)
![transformed-linear-combination](images/transformed-linear-combination.png)
*The coordinates of the vector after a linear transformation are the same linear combination of the transformed basis vectors*  

![transformed-coordinates](images/transformed-coordinates.png)

![matrix-basis-1](images/matrix-basis-1.png)
*We can forma a matrix whose columns are the basis vectors*

![matrix-basis-2](images/matrix-basis-2.png)
*We can calculate the coordinates of the transformed vector via the basis matrix-vector multiplication*

![determinant](images/determinant.png)
*The factor by which the area after the transformation is increased.The sign of the dererminant indicates the "flipping" of the transformed space*

![determinant-calc](images/determinant-calc.png)
*How to calculate the determinant.*

![rank](images/rank.png)
*The rank of the matrix is the positive integer that indicates the number of dimensions in the output of the transformation that involves this matrix.*

![column-space](images/column-space.png)
*The column space is the span of its column vectors (input space)*

![null-space](images/null-space.png)
*The null space is the space of all vectors that after the transformation land on the origin*

![2d-to-3d](images/transform-2d-3d.png)
*2D to 3D transformation. The column space includes two basis vectors. Three rows indicate that the basis vectors live in 3D.*



## Matrix Multiplication 

![matrix-multiplication](images/matrix-multiplication.png)
*Matrix multiplication can be seen as two consecutive linear transformations*

# Inverse Matrices

![linear-system-equations](images/linear-system-equations.png)

![meaning-linear-system](images/meaning-linear-system.png)
*Looking for an $x$ that when it is transformed by $A$, it will land on $v$ - picture depicts multiple $x$'s not the solution that will be on top of $v$*

![inverse-transformation](images/inverse-transformation.png)
*Looking at the reverse problem, we can start with $v$ and find the transformation that gives us $x$.This transformation is called the inverse of $A$: $A^{-1}$*

![existence-inverse](images/existence-inverse.png)
*Existence of inverse transformation*

![linear-system-solution](images/linear-system-solution.png)
*Solution to the linear system of equations*
