---
layout: post
title: Matplotlib Quick Start
categories: Dev
tags: [beginner, python]
---

# Introduction
matplotlib是Python語言及其數值計算庫NumPy的繪圖庫。它提供了一個物件導向的API，用於使用通用GUI工具包（如Tkinter、wxPython、Qt或GTK）將繪圖嵌入到應用程式中。

<!-- more -->

# Types of plots

| Function  | Description                                       |
| --------- | ------------------------------------------------- |
| bar       | Make a bar plot(長條圖).                          |
| barh      | Make a horizontal bar plot(橫長條圖).             |
| boxplot   | Make a box and whisker plot(箱形圖).              |
| hist      | Plot a histogram(直方圖).                         |
| hist2d    | Make a 2D histogram plot(2D直方圖).               |
| pie       | Plot a pie chart(派餅圖).                         |
| plot      | Plot lines and/or markers to the Axes(曲/折線圖). |
| polar     | Make a polar plot(極座標圖).                      |
| scatter   | Make a scatter plot of x vs y(散佈圖).            |
| stackplot | Draws a stacked area plot(堆疊面積圖).            |
| stem      | Create a stem plot(枝葉圖).                       |
| step      | Make a step plot(階梯圖).                         |
| quiver    | Plot a 2-D field of arrows(向量圖).               |

# Image functions

| Function | Description                              |
| -------- | ---------------------------------------- |
| imread   | Read an image from a file into an array. |
| imsave   | Save an array as in image file.          |
| imshow   | Display an image on the axes.            |

# Axis functions

| Function | Description                                                  |
| -------- | ------------------------------------------------------------ |
| axes     | Add axes to the figure.                                      |
| text     | Add text to the axes.                                        |
| title    | Set a title of the current axes.                             |
| xlabel   | Set the x axis label of the current axis.                    |
| xlim     | Get or set the x limits of the current axes.                 |
| xscale   | Set the scaling of the x-axis.                               |
| xticks   | Get or set the x-limits of the current tick locations and labels. |
| ylabel   | Set the y axis label of the current axis.                    |
| ylim     | Get or set the y-limits of the current axes.                 |
| yscale   | Set the scaling of the y-axis.                               |
| yticks   | Get or set the y-limits of the current tick locations and labels. |

# Figure functions

| Function | Description              |
| -------- | ------------------------ |
| figtext  | Add text to figure       |
| figure   | Creates a new figure.    |
| show     | Display a figure.        |
| savefig  | Save the current figure. |
| close    | Close a figure window.   |

# Plot sine wave

```python
import matplotlib.pyplot as plot
import numpy as np
import math #needed for definition of pi
# %matplotlib inline		required in jupyter notebook 
x = np.arange(0, math.pi*2, 0.05)
y = np.sin(x)
plt.plot(x,y)
plt.xlabel("angle")
plt.ylabel("sine")
plt.title('sine wave')
plt.show() # comment it in jupyter notebook
```

## Using object-oriented interface

```python
import matplotlib.pyplot as plot
import numpy as np
import math #needed for definition of pi
x = np.arange(0, math.pi*2, 0.05)
y = np.sin(x)
fig = plt.figure()
ax = fig.add_axes([0,0,1,1]) # A 4-length sequence of [left, bottom, width, height] quantities.
ax.plot(x,y)
ax.set_title("sine wave")
ax.set_xlabel('angle')
ax.set_ylabel('sine')
plt.show()
```

# Figure class

```python
fig = plt.figure()
```

## parameter

| name      |                                |
| --------- | ------------------------------ |
| Figsize   | (width,height) tuple in inches |
| Dpi       | Dots per inches                |
| Facecolor | Figure patch facecolor         |
| Edgecolor | Figure patch edge color        |
| Linewidth | Edge line width                |

# Axes class

```python
ax = fig.add_axes([0,0,1,1])
```

## legend

```python
ax.legend(handles, labels, loc)
```

| Location string | Location code |
| --------------- | ------------- |
| best            | 0             |
| upper right     | 1             |
| upper left      | 2             |
| lower left      | 3             |
| lower right     | 4             |
| right           | 5             |
| center left     | 6             |
| center right    | 7             |
| lower center    | 8             |
| upper center    | 9             |
| center          | 10            |

## axes.plot()

### Color code

| Character | Color   |
| --------- | ------- |
| 'b'       | blue    |
| 'g'       | green   |
| 'r'       | red     |
| 'c'       | cyan    |
| 'm'       | magenta |
| 'y'       | yellow  |
| 'k'       | black   |
| 'w'       | white   |

### Marker code

| Character | Description    |
| --------- | -------------- |
| '.'       | point marker   |
| 'o'       | circle marker  |
| 'x'       | x marker       |
| 'D'       | diamond marker |
| 'H'       | hexagon marker |
| 's'       | square marker  |
| '+'       | plus marker    |

### Line styles

| Character | Description   |
| --------- | ------------- |
| '-'       | solid line    |
| '--'      | dashed line   |
| '-.'      | dash-dot line |
| ':'       | dotted line   |

## Example

```python
import matplotlib.pyplot as plt

y = [1, 4, 9, 16, 25,36,49, 64]
x1 = [1, 16, 30, 42,55, 68, 77,88]
x2 = [1,6,12,18,28, 40, 52, 65]

fig=plt.figure()

ax=fig.add_axes([0,0,1,1])

l1=ax.plot(x1,y,'ys-') # solid line with yellow colour and square marker

l2=ax.plot(x2,y,'go--') # dash line with green colour and circle marker

ax.legend(labels=('tv', 'Smartphone'), loc='lower right') # legend placed at lower right
ax.set_title("Advertisement effect on sales")
ax.set_xlabel('medium')
ax.set_ylabel('sales')
plt.show()
```

# Miltiplots

```python
plt.subplot(subplot(nrows, ncols, index))
```
## Example 1
```python
import matplotlib.pyplot as plt

# plot a line, implicitly creating a subplot(111)
plt.plot([1,2,3])
# now create a subplot which represents the top plot of a grid with 2 rows and 1 column.
#Since this subplot will overlap the first, the plot (and its axes) previously created, will be removed
plt.subplot(211)
plt.plot(range(12))
plt.subplot(212, facecolor='y') # creates 2nd subplot with yellow background
plt.plot(range(12))
plt.show()
```
## Example 2
```python
import matplotlib.pyplot as plt

fig = plt.figure()

ax1 = fig.add_subplot(111)
ax1.plot([1,2,3])

ax2 = fig.add_subplot(221, facecolor='y')
ax2.plot([1,2,3])
plt.show()
```

## Example 3

```python
import matplotlib.pyplot as plt
import numpy as np
import math

x=np.arange(0, math.pi*2, 0.05)

fig=plt.figure()

axes1 = fig.add_axes([0.1, 0.1, 0.8, 0.8]) # main axes

axes2 = fig.add_axes([0.55, 0.55, 0.3, 0.3]) # inset axes

y=np.sin(x)

axes1.plot(x, y, 'b')
axes2.plot(x,np.cos(x),'r')

axes1.set_title('sine')
axes2.set_title("cosine")
plt.show()
```

## subplots()

```python
plt,subplots(nrows, ncols)
```

```python
import matplotlib.pyplot as plt
import numpy as np

fig, a = plt.subplots(2,2)

x=np.arange(1,5)

a[0][0].plot(x,x*x)
a[0][0].set_title('square')

a[0][1].plot(x,np.sqrt(x))
a[0][1].set_title('square root')

a[1][0].plot(x,np.exp(x))
a[1][0].set_title('exp')

a[1][1].plot(x,np.log10(x))
a[1][1].set_title('log')
plt.show()
```

## subplot2grid()

```python
plt.subplot2grid(shape, location, rowspan, colspan)
```

```python
import matplotlib.pyplot as plt
import numpy as np

a1 = plt.subplot2grid((3,3),(0,0),colspan=2)
a2 = plt.subplot2grid((3,3),(0,2), rowspan=3)
a3 = plt.subplot2grid((3,3),(1,0),rowspan=2, colspan=2)

x=np.arange(1,10)

a1.plot(x, np.exp(x))
a1.set_title('exp')

a2.plot(x, x*x)
a2.set_title('square')

a3.plot(x, np.log(x))
a3.set_title('log')
plt.tight_layout()
plt.show()
```

# Grids

```python
import matplotlib.pyplot as plt
import numpy as np

fig, axes = plt.subplots(1,3, figsize=(12,4))

x=np.arange(1,11)

axes[0].plot(x, x**3, 'g',lw=2)
axes[0].grid(True)
axes[0].set_title('default grid')

axes[1].plot(x, np.exp(x), 'r')
axes[1].grid(color='b', ls='-.', lw=0.25)
axes[1].set_title('custom grid')

axes[2].plot(x,x)
axes[2].set_title('no grid')
fig.tight_layout()
plt.show()
```

# Formatting axes

```python
import matplotlib.pyplot as plt
import numpy as np

fig, axes = plt.subplots(1, 2, figsize=(10,4))

x=np.arange(1,5)

axes[0].plot( x, np.exp(x))
axes[0].plot(x,x**2)
axes[0].set_title("Normal scale")

axes[1].plot (x, np.exp(x))
axes[1].plot(x, x**2)
axes[1].set_yscale("log")
axes[1].set_title("Logarithmic scale (y)")

axes[0].set_xlabel("x axis")
axes[0].set_ylabel("y axis")
axes[0].xaxis.labelpad = 10

axes[1].set_xlabel("x axis")
axes[1].set_ylabel("y axis")
plt.show()
```

## edge setting

```python
import matplotlib.pyplot as plt

fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

ax.spines['bottom'].set_color('blue')
ax.spines['left'].set_color('red')
ax.spines['left'].set_linewidth(2)
ax.spines['right'].set_color(None)
ax.spines['top'].set_color(None)
ax.plot([1,2,3,4,5])
plt.show()
```

# Setting limits

```python
import matplotlib.pyplot as plt
import numpy as np

fig = plt.figure()
a1 = fig.add_axes([0,0,1,1])

x = np.arange(1,10)
a1.plot(x, np.exp(x),'r')
a1.set_title('exp')
a1.set_ylim(0,10000)
a1.set_xlim(0,10)
plt.show()
```

# Setting ticks and tick labels

```python
import matplotlib.pyplot as plt
import numpy as np
import math

x = np.arange(0, math.pi*2, 0.05)
fig = plt.figure()
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8]) # main axes
y = np.sin(x)

ax.plot(x, y)
ax.set_xlabel(‘angle’)
ax.set_title('sine')
ax.set_xticks([0,2,4,6])
ax.set_xticklabels(['zero','two','four','six'])
ax.set_yticks([-1,0,1])
plt.show()
```

# Twin axes

```python
import matplotlib.pyplot as plt
import numpy as np

fig = plt.figure()
a1 = fig.add_axes([0,0,1,1])
x = np.arange(1,11)

a1.plot(x,np.exp(x))
a1.set_ylabel('exp')
a2 = a1.twinx()
a2.plot(x, np.log(x),'ro-')
a2.set_ylabel('log')
fig.legend(labels=('exp','log'),loc='upper left')
plt.show()
```

# Bar plot

```python
ax.bar(x, height, width, bottom, align)
```

## Parameter

| Name   | Description                                                  |
| ------ | ------------------------------------------------------------ |
| x      | sequence of scalars representing the x coordinates of the bars. align controls if x is the bar center (default) or left edge. |
| height | scalar or sequence of scalars representing the height(s) of the bars |
| width  | scalar or array-like, optional. the width(s) of the bars default 0.8 |
| bottom | scalar or array-like, optional. the y coordinate(s) of the bars default None |
| align  | {‘center’, ‘edge’}, optional, default ‘center’               |

## Example 1

```python
import matplotlib.pyplot as plt

fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

langs=['C', 'C++', 'Java', 'Python', 'PHP']
students=[23,17,35,29,12]
ax.bar(langs,students)
plt.show()
```

## Example 2

```python
import numpy as np
import matplotlib.pyplot as plt

data = [[30, 25, 50, 20],
		[40, 23, 51, 17],
		[35, 22, 45, 19]]
X = np.arange(4)

fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

ax.bar(X + 0.00, data[0], color = 'b', width = 0.25)
ax.bar(X + 0.25, data[1], color = 'g', width = 0.25)
ax.bar(X + 0.50, data[2], color = 'r', width = 0.25)
ax.set_xticks([0.25,1.25,2.25,3.25])
ax.set_xticklabels([2015,2016,2017,2018])
ax.legend(labels=['CS','IT','E&TC'])
plt.show()
```

## Example 3

```python
import numpy as np
import matplotlib.pyplot as plt

N = 5
width = 0.35 
menMeans = (20, 35, 30, 35, 27)
womenMeans = (25, 32, 34, 20, 25)
ind = np.arange(N) # the x locations for the groups

fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

ax.bar(ind, menMeans, width, color='r')
ax.bar(ind, womenMeans, width,bottom=menMeans, color='b')
ax.set_ylabel('Scores')
ax.set_title('Scores by group and gender')
ax.set_xticks(ind, ('G1', 'G2', 'G3', 'G4', 'G5'))
ax.set_yticks(np.arange(0, 81, 10))
ax.legend(labels=['Men', 'Women'])
plt.show()
```

# Histogram

```python
ax.hist(x, bins [,range, density, cumulative, histtype])
```

## Parameter

| Name       | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| x          | array or sequence of arrays                                  |
| bins       | integer or sequence or ‘auto’, optional                      |
| range      | The lower and upper range of the bins.                       |
| density    | If True, the first element of the return tuple will be the counts normalized to form a probability density |
| cumulative | If True, then a histogram is computed where each bin gives the counts in that bin plus all bins for smaller values. |
| histtype   | The type of histogram to draw. Default is ‘bar’              |

## Example
```python
import matplotlib.pyplot as plt
import numpy as np

fig,ax = plt.subplots(1,1)
a = np.array([22,87,5,43,56,73,55,54,11,20,51,5,79,31,27])

ax.hist(a, bins = [0,25,50,75,100])
ax.set_title("histogram of result")
ax.set_xticks([0,25,50,75,100])
ax.set_xlabel('marks')
ax.set_ylabel('no. of students')
plt.show()
```

# Pie chart

```python
ax.pie(x, labels, colors, autopct)
```

## Parameter

| Name    | Description                                                  |
| ------- | ------------------------------------------------------------ |
| x       | array-like. The wedge sizes.                                 |
| labels  | list. A sequence of strings providing the labels for each wedge |
| colors  | A sequence of matplotlibcolorargs through which the pie chart will cycle. If None, will use the colors in the currently active cycle. |
| autopct | string, used to label the wedges with their numeric value. The label will be placed inside the wedge. The format string will be fmt%pct. |

## Example
```python
import matplotlib.pyplot as plt
import numpy as np

fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

ax.axis('equal')
langs=['C', 'C++', 'Java', 'Python', 'PHP']
students=[23,17,35,29,12]

ax.pie(students, labels=langs,autopct='%1.2f%%')
plt.show()
```

# Scatter plot

## Example

```python
import matplotlib.pyplot as plt

girls_grades = [89, 90, 70, 89, 100, 80, 90, 100, 80, 34]
boys_grades = [30, 29, 49, 48, 100, 48, 38, 45, 20, 30]
grades_range = [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

ax.scatter(grades_range, girls_grades, color='r')
ax.scatter(grades_range, boys_grades, color='b')
ax.set_xlabel('Grades Range')
ax.set_ylabel('Grades Scored')
ax.set_title('scatter plot')
plt.show()
```

# Contour plot

## Example

```python
import numpy as np
import matplotlib.pyplot as plt

xlist = np.linspace(-3.0, 3.0, 100)
ylist = np.linspace(-3.0, 3.0, 100)
X, Y = np.meshgrid(xlist, ylist)
Z = np.sqrt(X**2 + Y**2)

fig,ax = plt.subplots(1,1)
cp = ax.contourf(X, Y, Z)
fig.colorbar(cp) # Add a colorbar to a plot
ax.set_title('Filled Contours Plot')
#ax.set_xlabel('x (cm)')
ax.set_ylabel('y (cm)')
plt.show()
```

# Quiver plot

```python
ax.quiver(x,y,u,v,c)
```

## Parameter

| Name | Description                                                  |
| ---- | ------------------------------------------------------------ |
| x    | 1D or 2D array, sequence. The x coordinates of the arrow locations |
| y    | 1D or 2D array, sequence. The y coordinates of the arrow locations |
| u    | 1D or 2D array, sequence. The x components of the arrow vectors |
| v    | 1D or 2D array, sequence. The y components of the arrow vectors |
| c    | 1D or 2D array, sequence. The arrow colors                   |

## Example

```python
import matplotlib.pyplot as plt
import numpy as np

x,y = np.meshgrid(np.arange(-2, 2, .2), np.arange(-2, 2, .25))
z = x*np.exp(-x**2 - y**2)
v, u = np.gradient(z, .2, .2)

fig, ax = plt.subplots()
q = ax.quiver(x,y,u,v)
plt.show()
```

# Box plot

## Example

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(10)
collectn_1 = np.random.normal(100, 10, 200)
collectn_2 = np.random.normal(80, 30, 200)
collectn_3 = np.random.normal(90, 20, 200)
collectn_4 = np.random.normal(70, 25, 200)
data_to_plot = [collectn_1, collectn_2, collectn_3, collectn_4]

fig = plt.figure()
# Create an axes instance
ax = fig.add_axes([0,0,1,1])
# Create the boxplot
bp = ax.boxplot(data_to_plot)
plt.show()
```

# Violin plot

## Example

```python
import matplotlib.pyplot as plt
import numpy as np

np.random.seed(10)
collectn_1 = np.random.normal(100, 10, 200)
collectn_2 = np.random.normal(80, 30, 200)
collectn_3 = np.random.normal(90, 20, 200)
collectn_4 = np.random.normal(70, 25, 200)
## combine these different collections into a list
data_to_plot = [collectn_1, collectn_2, collectn_3, collectn_4]

# Create a figure instance
fig = plt.figure()
# Create an axes instance
ax = fig.add_axes([0,0,1,1])
# Create the boxplot
bp = ax.violinplot(data_to_plot)
plt.show()
```

# Three-dimensional plotting

## Example

```python
import mpl_toolkits.mplot3d
import numpy as np
import matplotlib.pyplot as plt

fig = plt.figure()
ax = plt.axes(projection='3d')

z = np.linspace(0, 1, 100)
x = z * np.sin(20 * z)
y = z * np.cos(20 * z)
ax.plot3D(x, y, z, 'gray')
ax.set_title('3D line plot')
plt.show()
```

## Example 3D scatter plot

```python
import mpl_toolkits.mplot3d
import numpy as np
import matplotlib.pyplot as plt

fig = plt.figure()
ax = plt.axes(projection='3d')

z = np.linspace(0, 1, 100)
x = z * np.sin(20 * z)
y = z * np.cos(20 * z)
c = x + y
ax.scatter(x, y, z, c=c)
ax.set_title('3d Scatter plot')
plt.show()
```

# 3D contour plot

## Example

```python
import mpl_toolkits.mplot3d
import numpy as np
import matplotlib.pyplot as plt

def f(x, y):
	return np.sin(np.sqrt(x ** 2 + y ** 2))

x = np.linspace(-6, 6, 30)
y = np.linspace(-6, 6, 30)
X, Y = np.meshgrid(x, y)
Z = f(X, Y)

fig = plt.figure()
ax = plt.axes(projection='3d')
ax.contour3D(X, Y, Z, 50, cmap='binary')
ax.set_xlabel('x')
ax.set_ylabel('y')
ax.set_zlabel('z')
ax.set_title('3D contour')
plt.show()
```

# 3D wireframe plot

## Example

```python
import mpl_toolkits.mplot3d
import numpy as np
import matplotlib.pyplot as plt

def f(x, y):
	return np.sin(np.sqrt(x ** 2 + y ** 2))

x = np.linspace(-6, 6, 30)
y = np.linspace(-6, 6, 30)
X, Y = np.meshgrid(x, y)
Z = f(X, Y)

fig = plt.figure()
ax = plt.axes(projection='3d')
ax.plot_wireframe(X, Y, Z, color='black')
ax.set_title('wireframe')
plt.show()
```

# 3D surface plot

## Example

```python
import mpl_toolkits.mplot3d
import numpy as np
import matplotlib.pyplot as plt

x = np.outer(np.linspace(-2, 2, 30), np.ones(30))
y = x.copy().T # transpose
z = np.cos(x ** 2 + y ** 2)

fig = plt.figure()
ax = plt.axes(projection='3d')
ax.plot_surface(x, y, z,cmap='viridis', edgecolor='none')
ax.set_title('Surface plot')
plt.show()
```

# Working with text

## Parameter

| Name     | Description                                                  |
| -------- | ------------------------------------------------------------ |
| text     | Add text at an arbitrary location of the Axes.               |
| annotate | Add an annotation, with an optional arrow, at an arbitrary location of theAxes. |
| xlabel   | Add a label to the Axes’s x-axis.                            |
| ylabel   | Add a label to the Axes’s y-axis.                            |
| title    | Add a title to the Axes.                                     |
| figtext  | Add text at an arbitrary location of the Figure.             |
| suptitle | Add a title to the Figure.                                   |

## Example

```python
import matplotlib.pyplot as plt

fig = plt.figure()
ax = fig.add_axes([0,0,1,1])

ax.set_title('axes title')
ax.set_xlabel('xlabel')
ax.set_ylabel('ylabel')

ax.text(3, 8, 'boxed italics text in data coords', style='italic', bbox={'facecolor': 'red'})
ax.text(2, 6, r'an equation: $E=mc^2$', fontsize=15)
ax.text(4, 0.05, 'colored text in axes coords', verticalalignment='bottom', color='green', fontsize=15)

ax.plot([2], [1], 'o')
ax.annotate('annotate', xy=(2, 1), xytext=(3, 4), arrowprops=dict(facecolor='black', shrink=0.05))
ax.axis([0, 10, 0, 10])
plt.show()
```

# Mathematical expressions

You can use a subset TeXmarkup in any Matplotlib text string by placing it inside a pair of dollar signs ($).

```python
# math text
plt.title(r'$\alpha > \beta$')
```

## Example

```python
import numpy as np
import matplotlib.pyplot as plt

t = np.arange(0.0, 2.0, 0.01)
s = np.sin(2*np.pi*t)

plt.plot(t,s)
plt.title(r'$\alpha_i> \beta_i$', fontsize=20)
plt.text(0.6, 0.6, r'$\mathcal{A}\mathrm{sin}(2 \omega t)$', fontsize=20)
plt.text(0.1, -0.5, r'$\sqrt{2}$', fontsize=10)
plt.xlabel('time (s)')
plt.ylabel('volts (mV)')
plt.show()
```

# Working with images

## Example

```python
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
import numpy as np

img = mpimg.imread('mtplogo.png')
plt.imsave("logo.png", img, cmap='gray', origin='lower')
imgplot = plt.imshow(img)
```

