---
title: 什么是NumPy数组 (ndarray)？
description: np.array() 是 NumPy 库中最核心的函数之一，用于创建 NumPy 数组（Ndarray）。NumPy 是 Python 中进行科学计算的基础库，而 NumPy 数组是其处理数据的基本结构，它比 Python 原生的列表（list）在数值计算上效率更高、速度更快。
publishDate: 2025-12-06
---

NumPy 数组是一种多维、同质的数据容器。

-   **多维 (Multi-dimensional)**: 它可以表示向量（1D）、矩阵（2D）、甚至更高维的数据结构（如 RGB 图像是 3D 数组）。
-   **同质 (Homogeneous)**: 数组中所有元素必须是相同的数据类型（例如，都是整数、都是浮点数）。这是它比 Python 列表（可以包含不同类型数据）效率高的关键原因。

`np.array()` 函数的基本目的是将一个**可迭代对象**（如 Python 列表、元组等）转换为一个 NumPy 数组。

## 1. 语法和主要参数

最常用的语法如下：

```python
import numpy as np

np.array(object, dtype=None, copy=True, order='K', subok=False, ndmin=0)
```

| **参数**     | **描述**                                                     | **常用值/默认值** |
| ------------ | ------------------------------------------------------------ | ----------------- |
| **`object`** | 必需。任何可转换为数组的序列（列表、元组等）。               | -                 |
| **`dtype`**  | 可选。数组中元素的所需数据类型。                             | `None` (自动推断) |
| **`copy`**   | 可选。如果为 `True`，则始终复制输入对象；如果为 `False`，则仅在输入不是 `ndarray` 或 `dtype` 不匹配时复制。 | `True`            |
| **`ndmin`**  | 可选。指定结果数组的最小维度。                               | `0`               |

## 2. 用法示例

### 2.1 创建一维数组（向量）

将 Python 列表转换为一维 NumPy 数组。

```python
# 输入：Python 列表
my_list = [10, 20, 30, 40] 

# 输出：一维数组 (4个元素)
arr_1d = np.array(my_list)
# arr_1d 的形状 (shape) 是 (4,)
print(arr_1d) # [10 20 30 40]
```

### 2.2 创建二维数组（矩阵）

将嵌套的 Python 列表（代表行和列）转换为二维 NumPy 数组。

```python
# 输入：嵌套列表
my_list_2d = [[1, 2, 3], [4, 5, 6]]

# 输出：二维数组 (2行 x 3列)
arr_2d = np.array(my_list_2d)
# arr_2d 的形状 (shape) 是 (2, 3)
print(arr_2d) 
# [[1 2 3]
#  [4 5 6]]
```

### 2.3 指定数据类型 (`dtype`)

通过指定 `dtype` 参数，可以控制数组元素的数据类型，这对于内存管理和精确计算很重要。常用的数据类型包括 `'int32'`、`'float64'` 等。

```python
# 强制转换为 64 位浮点数
arr_float = np.array([1, 2, 3], dtype=np.float64) 
# arr_float 的 dtype 是 float64
print(arr_float) # [1. 2. 3.]
```

## 3. NumPy 数组的优势

与 Python 列表相比，使用 `np.array()` 创建的数组具有以下优势：

-   **向量化操作 (Vectorization):** NumPy 允许在整个数组上执行数学运算，而无需通过循环。这些操作在底层由优化过的 C/Fortran 代码执行，速度极快。

    ```python
    a = np.array([1, 2, 3])
    b = np.array([4, 5, 6])
    print(a + b) # [5 7 9]  (直接对应元素相加)
    ```

-   **内存连续性 (Memory Locality):** 数组的元素存储在内存中的连续块中，使得 CPU 访问数据更快。

-   **属性丰富:** NumPy 数组提供了许多有用的属性，如 **`.shape`**（维度）、**`.dtype`**（数据类型）和 **`.ndim`**（维数），方便进行数据检查和操作。