---
layout: post
title: Numpy Quick Start
categories: Dev
tags: [beginner, python]
---

# Introduction

NumPy是Python語言的一個擴充程式庫。
支援高階大量的維度陣列與矩陣運算，此外也針對陣列運算提供大量的數學函式函式庫。

<!-- more -->

# The Basics

## Important attributes of an ndarray

```python
import numpy as np 

a = np.arange(15).reshape(3,5) # a is 3*5 ndarray

a.shape # return (3,5)  

a.ndim # return 2 for a's dimension

a.dtype # return dtype('int64')

a.dtype.name # return 'int64' the datatype of elements in a

a.size # return 15 the number of elements in a

type(a) # return <type 'numpy.ndarray'>

b = np.array([6, 7, 8]) # create 1*3 ndarray
```

## Array creation

```python
import numpy as np

a = np.array(1, 2, 3, 4) # wrong
a = np.array([1, 2, 3, 4]) # right

a1 = np.arange(6) # 1d array
a2 = np.arange(12).reshape(4,3) # 2d array
a3 = np.arange(24).reshape(2,3,4) # 3d array

b = np.array([1, 2, 3], dtype=complex) # assign dtype=complex

np.zeros((3,4)) # 3*4 array filled with 0

np.ones((2,3,4), dtype=np.int16) # 2*3*4 array filled with 1 

np.empty((2,3)) # 2*3 array filled with  uninitiallized value

np.arange(10, 30, 5) # np.arange(start, end, step) 
np.arange(0, 2, 0.3) # step accepts float number
```

### Example

```python
import numpy as np
import matplotlib.pyplot as plt

np.linspace(0, 2, 9) # 9 numbers from 0 to 2
x = np.linspace(0, 2*np.pi, 100)
f = np.sin(x)

plt.plot(x,f)
plt.show()
```

# Basic operations

```python
import numpy as np

a = np.array([20,30,40,50])

b = np.arange(4) # array([0, 1, 2, 3])

c = a-b # array([20, 29, 38, 47])

b**2 # array([0, 1, 4, 9])

10*np.sin(a) 

a<35 # array([ True, True, False, False])
```

```python
A = np.array([[1,1],[0,1]])

b = np.array([[2,0],[3,4]])

A * B # elementwise product

A @ B # matrix product

A.dot(B) # another matrix product
```

```python
a = np.ones((2,3), dtype=int)

b = np.random.random((2,3))

c = np.exp(b+1j) # dtype of c is complex128

a *= 3

b += a

a += b #error, b is not automatically converted to integer type
```

```python
a = np.arange(6) # array([0, 1, 2, 3, 4, 5])

a.sum() # return 15

a.min() # return 0

a.max() # return 5

b = np.arange(12).reshape(3,4)

b.sum(axis=0) # sum of each column

b.min(axis=1) # min of each row

b.cumsum(axis=1) # cumulative sum along each row
```
## Create array from function
```python
import numpy as np
def f(x,y):
	return 10*x+y
b = np.fromfunction(f,(5,4),dtype=int)
>>> b
array([[ 0, 1, 2, 3],
	   [10, 11, 12, 13],
	   [20, 21, 22, 23],
	   [30, 31, 32, 33],
	   [40, 41, 42, 43]])

>>> b[2,3]
23
>>> b[0:5, 1] # each row in the second column of b
array([ 1, 11, 21, 31, 41])
>>> b[ : ,1] # equivalent to the previous example
array([ 1, 11, 21, 31, 41])
>>> b[1:3, : ] # each column in the second and third row of b
array([[10, 11, 12, 13],
	   [20, 21, 22, 23]])
```

# Shape manipulation

```python
import numpy as np

a = np.floor(10*np.random.random((3,4)))
>>> a
array([[ 2., 8., 0., 6.],
	   [ 4., 5., 1., 1.],
	   [ 8., 9., 3., 6.]])
>>> a.shape
(3, 4)
>>> a.ravel() # returns the array, flattened
array([ 2., 8., 0., 6., 4., 5., 1., 1., 8., 9., 3., 6.])
>>> a.reshape(6,2) # returns the array with a modified shape
array([[ 2., 8.],
	   [ 0., 6.],
	   [ 4., 5.],
	   [ 1., 1.],
	   [ 8., 9.],
	   [ 3., 6.]])
>>> a.T # returns the array, transposed
array([[ 2., 4., 8.],
	   [ 8., 5., 9.],
	   [ 0., 1., 3.],
	   [ 6., 1., 6.]])
>>> a.T.shape
(4, 3)
>>> a.shape
(3, 4)
```

# Stacking together  different arrays

```python
>>> a = np.floor(10*np.random.random((2,2)))
>>> a
array([[ 8., 8.],
	   [ 0., 0.]])

>>> b = np.floor(10*np.random.random((2,2)))
>>> b
array([[ 1., 8.],
	   [ 0., 4.]])

>>> np.vstack((a,b))
array([[ 8., 8.],
	   [ 0., 0.],
	   [ 1., 8.],
	   [ 0., 4.]])

>>> np.hstack((a,b))
array([[ 8., 8., 1., 8.],
	   [ 0., 0., 0., 4.]])

>>> np.column_stack((a,b)) # with 2D arrays
array([[ 8., 8., 1., 8.],
	   [ 0., 0., 0., 4.]])
```

```python
>>> a = np.array([4.,2.])
>>> b = np.array([3.,8.])
>>> np.column_stack((a,b)) # returns a 2D array
array([[ 4., 3.],
	   [ 2., 8.]])

>>> np.hstack((a,b)) # the result is different
array([ 4., 2., 3., 8.])

>>> a[:,np.newaxis] # this allows to have a 2D columns vector
array([[ 4.],
	   [ 2.]])

>>> np.column_stack((a[:,np.newaxis],b[:,np.newaxis]))
array([[ 4., 3.],
	   [ 2., 8.]])
>>> np.hstack((a[:,np.newaxis],b[:,np.newaxis])) # the result is the same
array([[ 4., 3.],
	   [ 2., 8.]])
```
## Splitting one array into several smaller ones
```python
>>> a = np.floor(10*np.random.random((2,12)))
>>> a
array([[ 9., 5., 6., 3., 6., 8., 0., 7., 9., 7., 2., 7.],
	  [ 1., 4., 9., 2., 2., 1., 0., 6., 2., 2., 4., 0.]])

>>> np.hsplit(a,3) # Split a into 3
[array([[ 9., 5., 6., 3.],
		[ 1., 4., 9., 2.]]),
 array([[ 6., 8., 0., 7.],
		[ 2., 1., 0., 6.]]),
 array([[ 9., 7., 2., 7.],
		[ 2., 2., 4., 0.]])]

>>> np.hsplit(a,(3,4)) # Split a after the third and the fourth column
[array([[ 9., 5., 6.],
		[ 1., 4., 9.]]),
 array([[ 3.],
		[ 2.]]),
 array([[ 6., 8., 0., 7., 9., 7., 2., 7.],
		[ 2., 1., 0., 6., 2., 2., 4., 0.]])]
```

# Fancy indexing and index tricks

```python
>>> a = np.arange(12)**2 # the first 12 square numbers
>>> i = np.array( [ 1,1,3,8,5 ] ) # an array of indices

>>> a[i] # the elements of a at the positions i
array([ 1, 1, 9, 64, 25])

>>> j = np.array( [ [ 3, 4], [ 9, 7 ] ] ) # a bidimensional array of indices

>>> a[j] # the same shape as j
array([[ 9, 16],
	   [81, 49]])

>>> a = np.arange(12).reshape(3,4)
>>> a
array([[ 0, 1, 2, 3],
	   [ 4, 5, 6, 7],
	   [ 8, 9, 10, 11]])

>>> i = np.array( [ [0,1], [1,2] ] ) # indices for the first dim of a

>>> j = np.array( [ [2,1], [3,3] ] ) # indices for the second dim

>>> a[i,j] # i and j must have equal shape
array([[ 2, 5],
	   [ 7, 11]])
```

```python
>>> a = np.arange(12).reshape(3,4)
>>> b = a > 4
>>> b # b is a boolean with a's shape
array([[False, False, False, False],
	   [False, True, True, True],
	   [ True, True, True, True]])
>>> a[b] # 1d array with the selected elements
array([ 5, 6, 7, 8, 9, 10, 11])

>>> a[b] = 0 # All elements of 'a' higher than 4 become 0
>>> a
array([[0, 1, 2, 3],
       [4, 0, 0, 0],
	   [0, 0, 0, 0]])
```

# Mandelbrot set

```python
import numpy as np
import matplotlib.pyplot as plt

>>> def mandelbrot( h,w, maxit=20 ):
	 """Returns an image of the Mandelbrot fractal of size (h,w)."""
	y,x = np.ogrid[ -1.4:1.4:h*1j, -2:0.8:w*1j ]
	c = x+y*1j
	z = c
	divtime = maxit + np.zeros(z.shape, dtype=int)
    
	for i in range(maxit):
		z = z**2 + c
		diverge = z*np.conj(z) > 2**2 # who is diverging
		div_now = diverge & (divtime==maxit) # who is diverging now
		divtime[div_now] = i # note when
		z[diverge] = 2 # avoid diverging too much
        
	return divtime

>>> plt.imshow(mandelbrot(400,400))
>>> plt.show()
```

# The ix_() function

```python
>>> a = np.array([2,3,4,5])
>>> b = np.array([8,5,4])
>>> c = np.array([5,4,6,8,3])

>>> ax,bx,cx = np.ix_(a,b,c)
>>> ax
array([[[2]],
	   [[3]],
	   [[4]],
	   [[5]]])

>>> bx
array([[[8],
		[5],
		[4]]])

>>> cx
array([[[5, 4, 6, 8, 3]]])

>>> ax.shape, bx.shape, cx.shape
((4, 1, 1), (1, 3, 1), (1, 1, 5))

>>> result = ax+bx*cx

>>> result
array([[[42, 34, 50, 66, 26],
		[27, 22, 32, 42, 17],
		[22, 18, 26, 34, 14]],
	   [[43, 35, 51, 67, 27],
		[28, 23, 33, 43, 18],
		[23, 19, 27, 35, 15]],
	   [[44, 36, 52, 68, 28],
		[29, 24, 34, 44, 19],
		[24, 20, 28, 36, 16]],
	   [[45, 37, 53, 69, 29],
		[30, 25, 35, 45, 20],
		[25, 21, 29, 37, 17]]])

>>> result[3,2,4]
17
>>> a[3]+b[2]+c[4]
17
```

# Linear algebra

```python
import numpy as np

>>> a = np.array([[1.0, 2.0], [3.0, 4.0]])
>>> print(a)
	[[ 1. 2.]
	 [ 3. 4.]]
    
>>> a.transpose()
array([[ 1., 3.],
	   [ 2., 4.]])

>>> np.linalg.inv(a)
array([[-2. , 1. ],
	   [ 1.5, -0.5]])

>>> u = np.eye(2) # unit 2x2 matrix; "eye" represents "I"
>>> u
array([[ 1., 0.],
	   [ 0., 1.]])

>>> j = np.array([[0.0, -1.0], [1.0, 0.0]])
>>> j @ j # matrix product
array([[-1., 0.],
	   [ 0., -1.]])

>>> np.trace(u) # trace
2.0

>>> y = np.array([[5.], [7.]])
>>> np.linalg.solve(a, y)
array([[-3.],
	   [ 4.]])

>>> np.linalg.eig(j)
(array([ 0.+1.j, 0.-1.j]),
 array([[ 0.70710678+0.j , 0.70710678-0.j ],
		[ 0.00000000-0.70710678j, 0.00000000+0.70710678j]]))
```

# Histograms

```python
import numpy as np
import matplotlib.pyplot as plt
# Build a vector of 10000 normal deviates with variance 0.5^2 and mean 2
>>> mu, sigma = 2, 0.5
>>> v = np.random.normal(mu,sigma,10000)

>>> # Plot a normalized histogram with 50 bins
>>> plt.hist(v, bins=50, density=1) # matplotlib version (plot)
>>> plt.show()

>>> # Compute the histogram with numpy and then plot it
>>> (n, bins) = np.histogram(v, bins=50, density=True) # NumPy version (no plot)
>>> plt.plot(.5*(bins[1:]+bins[:-1]), n)
>>> plt.show()
```

