
---
title: Matplotlib基本语法
date: 2019-06-24
id: 1
categories: [基本语法]
---

## 基本配置与标记


```python
import numpy as np
import matplotlib.pyplot as plt

# 基本配置
plt.figure(figsize = (10, 10), dpi = 80)
plt.xlim(-4.0, 4.0) # 坐标上下限
plt.ylim(-1.0, 1.0)
'''
plt.xticks(np.linspace(-4, 4, 9, endpoint = True))
plt.yticks(np.linspace(-1, 1, 5, endpoint = True))
'''
# 更直观的记号
plt.xticks([-np.pi, -np.pi/2, 0, np.pi/2, np.pi], [r'$-\pi$', r'$-\pi/2$', r'$0$', r'$+\pi/2$', r'$+\pi$'])
plt.yticks([-1, 0, +1], [r'$-1$', r'$0$', r'$+1$'])

# 画曲线
X = np.linspace(-np.pi, np.pi, 256,endpoint = True)
Cos,Sin = np.cos(X), np.sin(X)
plt.plot(X, Cos, color = 'blue', linewidth = 1.0, linestyle = '-', label = 'cos') # label添加图例
plt.plot(X, Sin, color = 'green', linewidth = 1.0, linestyle = '-', label = 'sin')
plt.legend(loc='upper left') # 图例位置左上角

# 移动坐标
ax = plt.gca()
ax.spines['top'].set_color('none')
ax.spines['right'].set_color('none')
ax.xaxis.set_ticks_position('bottom')
ax.spines['bottom'].set_position(('data',0))
ax.yaxis.set_ticks_position('left')
ax.spines['left'].set_position(('data',0))

# 给特殊点加注释
t = 2*np.pi/3
plt.plot([t, t],[0, np.cos(t)], color = 'blue', linewidth = 2.5, linestyle = '--')
plt.scatter([t, ],[np.cos(t),], 50, color ='red')
plt.annotate(r'$\cos(\frac{2\pi}{3})=-\frac{1}{2}$',
            xy = (t, np.cos(t)), xycoords = 'data',
            xytext = (-90, -50), textcoords = 'offset points', fontsize = 16,
            arrowprops = {'arrowstyle':'->', 'connectionstyle':'arc3,rad=.2'})
plt.plot([t,t],[0,np.sin(t)], color ='red', linewidth=2.5, linestyle="--")
plt.scatter([t,],[np.sin(t),], 50, color ='red')
plt.annotate(r'$\sin(\frac{2\pi}{3})=\frac{\sqrt{3}}{2}$',
            xy = (t, np.sin(t)), xycoords = 'data',
            xytext = (+10, +30), textcoords = 'offset points', fontsize = 16,
            arrowprops = {'arrowstyle':'->', 'connectionstyle':'arc3,rad=.2'})

# 显示图片
plt.show()
```


![png](2019-06-24_Matplotlib基本语法output/output_2_0.png)


## 散布图


```python
import numpy as np
import matplotlib.pyplot as plt

n = 1024
X = np.random.normal(0, 1, n)
Y = np.random.normal(0, 1, n)

plt.scatter(X,Y)
plt.show()
```


![png](2019-06-24_Matplotlib基本语法output/output_4_0.png)


## 柱状图


```python
import numpy as np
import matplotlib.pyplot as plt

n = 12
X = np.arange(n)
Y1 = (1- X / float(n)) * np.random.uniform(0.5, 1.0, n)
Y2 = (1- X/ float(n)) * np.random.uniform(0.5, 1.0, n)

plt.axes([0.025, 0.025, 0.95, 0.95])
plt.bar(X, +Y1, facecolor = '#9999ff', edgecolor = 'white')
plt.bar(X, -Y2, facecolor = '#ff9999', edgecolor = 'white')

for x,y in zip(X,Y1):
    plt.text(x, y + 0.08, '%.2f' % y, ha = 'center', va = 'bottom')

for x,y in zip(X,Y2):
    plt.text(x, -y - 0.08, '%.2f' % y, ha = 'center', va= 'top')

plt.xlim(-.5, n), 
plt.ylim(-1.25, +1.25), 
plt.xticks([])
plt.yticks([])

plt.show()
```


![png](2019-06-24_Matplotlib基本语法output/output_6_0.png)


## 3D图


```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure()
ax = Axes3D(fig)
X = np.arange(-4, 4, 0.25)
Y = np.arange(-4, 4, 0.25)
X, Y = np.meshgrid(X, Y)
R = np.sqrt(X ** 2 + Y ** 2)
Z = np.sin(R)

ax.plot_surface(X, Y, Z, rstride = 1, cstride=1, cmap = plt.cm.hot)
ax.contourf(X, Y, Z, zdir = 'z', offset = -2, cmap = plt.cm.hot)
ax.set_zlim(-2,2)

plt.show()
```


![png](2019-06-24_Matplotlib基本语法output/output_8_0.png)


> 参考：

1. [廖雪峰Python数据分析](https://www.julyedu.com/course/getDetail/66/)