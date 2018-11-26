# Expletics: Full strength data modeling using python

**Current supported time series features**
* Dynamic Time Warping
* Linear Regression

**Installation**
* Prebuilt binaries for Python version 2.7, 64 bit [dist/](https://github.com/jaredbebb/expletics/tree/master/expletics/dist)
  * pip install dist/expletics-0.0.0-cp27-cp27m-win_amd64.whl
* for other python versions see [setup.py](https://github.com/jaredbebb/expletics/blob/master/expletics/setup.py)


**Tutorial**

```python
from linear_model import linear_model as LM
lm = LM()
x = [0,1,2,3,4,5,6,7,8,9]
y = [5,10,25,30,40,50,65,70,80,90]

lm.LinearRegression(x, y)
print"a:",lm.a
print"b:",lm.b
print"score:",lm.score
```

a: 3.0

b: 9.66666666667

score: 0.994410405246

```python
import matplotlib.pyplot as plt
plt.plot(x, y, 'bo')
plt.plot([0,x[len(x)-1]], [lm.a,x[len(x)-1]*lm.b], 'r--')
plt.legend(['count',' y = '+str(lm.a)+'x+ '+str(lm.b)+', R2='+str(lm.score)], loc='upper left')
plt.show()


x = [1,2,3,4,5,6,7]
trendup = [0.0, 0.0, 0.0, 2.0, 4.0,8.0,16.0]
trendflat = [16.0, 16.0, 16.0, 16.0, 16.0, 16.0, 16.0]
trenddown =[16.0,8.0,4.0,2.0,0.0,0.0,0.0]
week1_count = [0.0, 0.0, 0.0, 4.0, 8.0,16.0,32.0]
week2_count = [32.0,16.0,8.0,4.0, 0.0, 0.0,0.0 ]
week3_count = [0.0, 0.0, 1.0, 2.0, 5.0,6.0,6.0]

plt.plot(x, trendup,'k--')
plt.plot(x, trenddown, 'r--')
plt.plot(x, week1_count,'ko')
plt.plot(x, week2_count, 'm^')
plt.plot(x, week3_count, 'c^')
plt.legend(['trendup', 'trenddown', 'week1 count', 'week1 count','week3 count'], loc='center left',bbox_to_anchor=(1, 0.5))
plt.show()

from expletics.dtw import dtw
up = dtw(week1_count,trendup)
down = dtw(week1_count,trenddown)
trending = down/up > 1.0
print(trending)

up = dtw(week2_count,trendup)
down = dtw(week2_count,trenddown)
trending = down/up > 1.0
print(trending)

up = dtw(week3_count,trendup)
down = dtw(week3_count,trenddown)
trending = down/up > 1.0
print(trending)
```
True

False

True

**Information**
* Expletics is built using Cython for speed.
* C++ extensions for python
* Project is under development