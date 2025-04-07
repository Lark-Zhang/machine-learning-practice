# 机器学习入门练习
## 使用梯度下降法实现数字图像识别

### 感知器
一个感知器接受多个二进制输入 $x_1, x_2,...$，并产生二进制输出：

![](https://latex.codecogs.com/svg.latex?\text{output}=%20\begin{cases}%200%20&%20\text{if%20}%20\sum_{j}%20w_jx_j%20\leq%20\text{threshold}%20\\%201%20&%20\text{if%20}%20\sum_{j}%20w_jx_j%20>%20\text{threshold}%20\end{cases})

通过预设权重和偏置可设计逻辑电路，但无法自动学习。

---

### S型神经元
使用 σ 函数（Sigmoid）作为激活函数，输出随权重/偏置的微小变化而平滑变化：

![](https://latex.codecogs.com/svg.latex?\Delta\text{output}\approx\sum_j%20\frac{\partial\text{output}}{\partial%20w_j}\Delta%20w_j%20+%20\frac{\partial\text{output}}{\partial%20b}\Delta%20b)

---

### 神经网络架构
- ​**​前馈神经网络​**​：输入层 → 隐藏层（可多层） → 输出层  
- 每层神经元与下一层全连接

---

### 损失函数（均方误差）
定义损失函数量化模型拟合效果：

![](https://latex.codecogs.com/svg.latex?C(w,b)%20\equiv%20\frac{1}{2n}%20\sum_x%20\|y(x)-a\|^2)

其中：
- `w`：所有权重集合
- `b`：所有偏置集合
- `n`：训练数据个数
- `a`：输入为 `x` 时的输出向量

---

### 梯度下降法
#### 核心思想
通过负梯度方向更新参数以最小化损失函数：

![](https://latex.codecogs.com/svg.latex?\Delta%20v%20=%20-\eta%20\nabla%20C)  
（其中 ![](https://latex.codecogs.com/svg.latex?\eta) 为学习率）

#### 算法优化
采用​**​随机梯度下降 (SGD)​**​：每次迭代随机选取小批量样本 (`m` 个) 计算梯度近似值：

![](https://latex.codecogs.com/svg.latex?\frac{1}{m}\sum_{j=1}^m%20\nabla%20C_{X_j}%20\approx%20\nabla%20C)

---

### 实现说明
- ​**​激活函数​**​：使用 Sigmoid 函数实现非线性变换  
- ​**​学习率调整​**​：动态调整 ![](https://latex.codecogs.com/svg.latex?\eta) 以平衡收敛速度与稳定性  
- ​**​代码依赖​**​：需安装 `numpy` 和 `matplotlib`

> 注：公式图片由 [CodeCogs Equation Editor](https://latex.codecogs.com/) 生成，完整 LaTeX 源码可查看项目文件。
