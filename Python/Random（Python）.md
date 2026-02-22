# Random —— python（And）numpy

## Python内置Random库

### 一、导入random库

```python
import random
```

### 二、生成随机的浮点数

1. 使用`random.random()`可以直接生成一个`[0, 1]`之间的随机浮点数。
2. 使用`random.uniform(start, end)`可以指定生成`[start, end]`之间的随机浮点数。

```python
rand_float = random.random()   # 默认生成的是0 - 1之间的浮点数
print(rand_float)
rand_float = random.uniform(1.0, 10.0)   # 指定生成1 - 10之间的浮点数
print(rand_float)
```

### 三、生成随机的整数

1. 使用`random.randint(start, end)`可以生成`[start, end]`之间的随机整数。
2. 使用`random.randrange(start, end, step)`可以生成`[start, end]`之间，步长为5的随机整数。

```python
rand_int = random.randint(1, 10)    # 生成0 - 1之间的整数
print(rand_int)
rand_int = random.randrange(0, 101, 5)   # 生成0 - 101之间5的倍数的随机整数
print(rand_int)
```

### 四、随机选择元素

1. 使用`random.choice(sequence)`可以从传入的sequence（序列）中随机选择一个元素。
2. 使用`random.sample(sequence, num)`可以从sequence（序列）中随机选择num个元素，返回一个列表。

```python
elements = ['apple', 'banana', 'cherry']
element = random.choice(elements)   # 随机选择一种水果
print(element)
selected = random.sample(range(100), 10)  # 从0 - 99中随机选择10个不重复的数
print(selected)
```

### 五、随机种子

- 随机种子的意义：在不同的地方，如果使用相同的随机种子，并且进行相同数量随机数生成操作，那么会得到一个完全相同的随机数序列。

- 通过使用`random.seed(num)`来设定随机种子。

```python
random.seed(1)     # 初始设定随机种子为1，并且生成一个随机数赋值给a
a = random.randint(1, 10)
print(a)
random.seed(1)    # 在次生成随机数之前，设定随机种子为1，并且生成一个随机数赋值给b，将会得到随机数的结果a与b相同。
b = random.randint(1, 10)
print(b)
```

### 六、随机排列元素

- 使用`random.shuffle(sequence)`可以将sequence（序列）随机打乱。

```python
list_item = [1, 2, 3, 4, 5]
random.shuffle(list_item)
list_item
```

### 七、指定位数的随机数（整数）

- 使用`random.getrandbits(num)`可以生成num个二进制位的随机数值。生成随机数的范围是：$[0, 2^{num} - 1]$。

```python
bits = random.getrandbits(10)   # 获取10位的随机整数
print(bits)
```

### 八、从分布中取随机数

1. 使用`random.gauss(mean, std)`可以从一个均值为mean，标准差为std的分布中去一个随机数。特例：`random.gauss(0, 1)`表示从一个正太分布中取一个随机变量。
2. 使用`random.paretovariate(alpha, theta=1)`可以从Pareto Ⅱ分布中取一个随机数，其参数 $\theta$ 默认为1。

```python
normal_variate = random.gauss(0, 1)   # 标准正太分布随机变量
normal_variate
```

```python
pareto_variate = random.paretovariate(1.5)   # pareto 分布的随机变量
pareto_variate
```

### 九、通过指定权重来随机选择

- 使用`random.choice(sequence: list, weights: list)`方法可以通过设定sequence（序列）的权重，来进行随机选择。

```python
weighted_elements = random.choices(['red', 'blue', 'green'], weights=[2, 1, 1])   # 根据权重选择元素
weighted_elements
```

## numpy中的随机数

### 一、导入numpy库：

```python
import numpy as np
```

### 二、生成随机数：

1. **标准正态分布**：
   
   - 使用`np.random.randn(d0, d1, ..., dn)`方法可以生成具有给定形状的数组，数组中的元素来自标准正态分布（均值为0，标准差为1）。
   
   ```python
   standard_normal = np.random.randn()  # 单个标准正态分布随机数
   array_normal = np.random.randn(3, 4)  # 3x4数组，元素来自标准正态分布
   ```
   
2. **均匀分布**：
   
   - 使用`np.random.rand(d0, d1, ..., dn)`方法可以生成在 $[0, 1) $区间内均匀分布的随机数。
   
   ```python
   uniform_random = np.random.rand()  # 单个[0, 1)区间的随机数
   uniform_array = np.random.rand(2, 2)  # 2x2数组，元素在[0, 1)区间
   ```
   
3. **随机整数**：
   - 使用`np.random.randint(low, high, size, dtype)`方法可以生成一个或多个随机整数，范围从 `low`（包含）到 `high`（不包含）。

   ```python
   random_int = np.random.randint(1, 10)  # 1到9之间的随机整数
   random_int_array = np.random.randint(1, 100, size=5)  # 5个1到99之间的随机整数
   ```

### 三、分布采样：

NumPy `random` 模块提供了多种概率分布的采样函数，以下是一些例子：

1. **正态分布**：
   
   - 使用`np.random.normal(loc=0.0, scale=1.0, size=None)`方法可以从具有指定均值 `loc` 和标准差 `scale` 的正态分布中生成随机数。
   
   ```python
   normal_samples = np.random.normal(0, 1, 1000)  # 均值为0，标准差为1的1000个随机数
   ```
   
2. **二项分布**：
   - 使用`np.random.binomial(n, p, size=None)`方法可以从具有指定参数 `n` 和成功概率 `p` 的二项分布中生成随机数。

   ```python
   binomial_samples = np.random.binomial(100, 0.5, 10)  # n=100, p=0.5的10个随机数
   ```

3. **泊松分布**：
   - 使用`np.random.poisson(lam=1.0, size=None)`方法可以从具有指定平均值 `lam` 的泊松分布中生成随机数。

   ```python
   poisson_samples = np.random.poisson(lam=4, size=10)  # 平均值为4的10个随机数
   ```

4. **指数分布**：
   - 使用`np.random.exponential(scale=1.0, size=None)`方法可以从具有指定比例参数 `scale` 的指数分布中生成随机数。

   ```python
   exponential_samples = np.random.exponential(scale=1, size=5)  # 比例参数为1的5个随机数
   ```

### 四、随机排列和选择：

1. **随机排列**：
   - 使用`np.random.shuffle(x)`方法可以将序列 `x` 中的元素随机打乱位置。

   ```python
   list_items = [1, 2, 3, 4, 5]
   np.random.shuffle(list_items)  # 打乱列表元素的顺序
   ```

2. **随机选择**：
   
   - 使用`np.random.choice(a, size=None, replace=True, p=None)`方法可以从 `a` 中选择元素，可以是有放回或无放回的。
   
   ```python
   choice = np.random.choice([1, 2, 3, 4, 5])  # 随机选择一个元素
   choices = np.random.choice([1, 2, 3, 4, 5], size=2, replace=True)  # 有放回地随机选择两个元素
   ```

### 五、设置随机数生成器的种子：

- 通过`np.random.seed(seed=None)`方法来设置随机数生成器的种子，以确保结果的可重复性。

```python
np.random.seed(0)  # 设置随机数生成器的种子
```