# Python Tips

[toc]

python将字符串转化为时间： 

```python
datetime.strptime("08:01:45.5", '%H:%M:%S.%f')
```



Python string format:

| 数字       | 格式                                                         | 输出                   | 描述                         |
| ---------- | ------------------------------------------------------------ | ---------------------- | ---------------------------- |
| 3.1415926  | {:.2f}                                                       | 3.14                   | 保留小数点后两位             |
| 3.1415926  | {:+.2f}                                                      | +3.14                  | 带符号保留小数点后两位       |
| -1         | {:+.2f}                                                      | -1.00                  | 带符号保留小数点后两位       |
| 2.71828    | {:.0f}                                                       | 3                      | 不带小数                     |
| 5          | {:0>2d}                                                      | 05                     | 数字补零 (填充左边, 宽度为2) |
| 5          | {:x<4d}                                                      | 5xxx                   | 数字补x (填充右边, 宽度为4)  |
| 10         | {:x<4d}                                                      | 10xx                   | 数字补x (填充右边, 宽度为4)  |
| 1000000    | {:,}                                                         | 1,000,000              | 以逗号分隔的数字格式         |
| 0.25       | {:.2%}                                                       | 25.00%                 | 百分比格式                   |
| 1000000000 | {:.2e}                                                       | 1.00e+09               | 指数记法                     |
| 13         | {:>10d}                                                      | 13                     | 右对齐 (默认, 宽度为10)      |
| 13         | {:<10d}                                                      | 13                     | 左对齐 (宽度为10)            |
| 13         | {:^10d}                                                      | 13                     | 中间对齐 (宽度为10)          |
| 11         | `'{:b}'.format(11) '{:d}'.format(11) '{:o}'.format(11) '{:x}'.format(11) '{:#x}'.format(11) '{:#X}'.format(11)` | `1011 11 13 b 0xb 0XB` | 进制                         |

- ^, <, > 分别是居中、左对齐、右对齐，后面带宽度， : 号后面带填充的字符，只能是一个字符，不指定则默认是用空格填充。

- \+ 表示在正数前显示 +，负数前显示 -； （空格）表示在正数前加空格

- b、d、o、x 分别是二进制、十进制、八进制、十六进制。
- string format display math {}, using {{}}



Python run terminal commands:

```python
import subprocess
bashcmd = '/usr/local/bin/todo.sh ls -d /Users/cjhang/.config/todo/todo.cfg'
bashcmd = '/usr/local/bin/todo.sh -d /Users/cjhang/.config/todo/todo.cfg ls'
process = subprocess.Popen(bashcmd.split(), stdout=subprocess.PIPE)
process.communicate()
```



The usage of @

```python
def decorator(func):
    return func

@decorator
def some_func():
    pass
```

Is equivalent to:

```python
def decorator(func):
    return func

def some_func():
    pass

some_func = decorator(some_func)
```

In the definition of a decorator you can add some modified things that wouldn't be returned by a function normally.

```python
a@b
# equivalent to
dot(a, b)
```



**Memory Optimize**

python `__slots__` can be used for memory optimize



[Python deal with memories](https://realpython.com/python-memory-management/)

multi-processing: Try setting the maxtasksperchild argument on the pool



### Suppress the unwanted output

```python
import sys
import os

old_stdout = sys.stdout # backup current stdout
sys.stdout = open(os.devnull, "w")

my_nasty_function()

sys.stdout = old_stdout # reset old stdout
```

[ref](https://stackoverflow.com/questions/8447185/to-prevent-a-function-from-printing-in-the-batch-console-in-python)



## Numpy

Numpy make structured array:

```python
# numpy structured array:
x = np.array([('Rex', 9, 81.0), ('Fido', 3, 27.0)],
             dtype=[('name', 'U10'), ('age', 'i4'), ('weight', 'f4')])
```

 ```python
numpy.repeat # 可以重复列和行
numpy.roll   # 可以左右滚动列
numpy.tile   #
numpy.ravel  # return a contiguous flattened array
 ```

copy 2d array into repeat 3d array, also see the [discussion of broadcast](https://stackoverflow.com/questions/32171917/copy-2d-array-into-3rd-dimension-n-times-python)

```python
a = np.array([[1, 2], [1, 2]])
print(a.shape)
# (2,  2)
# indexing with np.newaxis inserts a new 3rd dimension, which we then repeat the
# array along, (you can achieve the same effect by indexing with None, see below)
b = np.repeat(a[:, :, np.newaxis], 3, axis=2)
print(b.shape)
# (2, 2, 3)
```



Clip

```python
a = 1 if k == 0 else 2
a[::2], a[1::2], every third element, a[star: end: step]
numpy.clip(a, a_min, a_max) #clip a into range [a_min, a_max]
```





## IPython

You can do %xdel testcube to delete the variable and remove it from IPython's cache. Alternatively, %reset out or %reset array will clear either all your output history, or only references to numpy arrays.

 Conda  install Jupiter and extensions:

```shell
conda install -c conda-forge jupyter_contrib_nbextensions
conda install -c conda-forge jupyter_nbextensions_configurator
```





## Error Handling:

general

```python
try:
    #your code
except Exception as ex:
    print(ex)
```

catch multiple expectations

```python
except (Exception1, Exception2) as e:
    pass
```

handle specific error

```python
try:
    file = open('input-file', 'open mode')
except (IOError, EOFError) as e:
    print("Testing multiple exceptions. {}".format(e.args[-1]))
		
try:
    file = open('input-file', 'open mode')
except EOFError as ex:
    print("Caught the EOF error.")
    raise ex
except IOError as e:
    print("Caught the I/O error.")
    raise ex

```

else,  run when no except encounter

```python
while True:
    # Enter integer value from the console.
    x = int(input())
		    # Divide 1 by x to test error cases
    try:
        result = 1 / x
    except:
        print("Error case")
        exit(0)
    else:
        print("Pass case")
        exit(1)

```

finally, always run

```python
try:   
    # Intentionally raise an error.   
    x = 1 / 0 
except:   
    # Except clause:   
    print("Error occurred") 
finally:   
    # Finally clause:   
    print("The [finally clause] is hit")
```

common errors

```python
except IOError: print('Error occurred while opening the file.')
except ValueError: print('Non-numeric input detected.')
except ImportError: print('Unable to locate the module.')
except EOFError: print('Identified EOF error.')
except KeyboardInterrupt: print('Wrong keyboard input.')
except: print('An error occurred.')
```





## Code snippets

[Loop in a spiral](https://stackoverflow.com/questions/398299/looping-in-a-spiral)

```python
def spiral(X, Y):
    x = y = 0
    dx = 0
    dy = -1
    for i in range(max(X, Y)**2):
        if (-X/2 < x <= X/2) and (-Y/2 < y <= Y/2):
            print (x, y)
            # DO STUFF...
        if x == y or (x < 0 and x == -y) or (x > 0 and x == 1-y):
            dx, dy = -dy, dx
        x, y = x+dx, y+dy
```



```python
fig.savefig('./results/results.png', bbox_inches='tight')
```



## Ipython

```python
# auto reload the packages
%load_ext autoreload
%autoreload 2
```

Import package in the upper level:

```python
import sys
sys.path.append("..")
```



