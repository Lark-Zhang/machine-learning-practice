按照机器学习-入门的练习
==============

### 1.使用梯度下降法实现简单的数字图像识别
#### 感知器

一个感知器接受几个二进制输入,$x_1,x_2,...$,并产生一个二进制输出:
$$ \text{output} = \begin{cases} 0 & \text{if } \sum_{j} w_{j}x_{j} \leq \text{threshold} \\ 1 & \text{if } \sum_{j} w_{j}x_{j} > \text{threshold} \end{cases} $$
通过预先设计权重和偏置可以设计逻辑电路,但是无法自动学习.
#### S型神经元

使用$\sigma$函数作为激活函数,可以实现输出反映权重和偏置的微小变化
$$ \Delta \text{output} \approx \sum_{j} \frac{\partial \text{output}}{\partial w_{j}} \Delta w_{j} + \frac{\partial \text{output}}{\partial b} \Delta b $$
#### 神经网络的架构

前馈神经网络:输入层、隐藏层、输出层
#### 损失函数

定义损失函数来描述量化模型的拟合效果
$$C(w,b) \equiv \frac{1}{2n} \sum_{x} \|y(x) - a\|^2$$
其中,$w$表示所有的网格中权重规定集合,$b$是所有的偏置,n是训练输入数据的个数,a是表示当输入为x时输出的向量.或称**均方误差**或者**MSE**.
#### 梯度下降法学习

训练的目的:找到最小化$C(w,b)$的权重和偏置.
假设$C=C(v_1,v_2)$
$$ \Delta C \approx  \frac{\partial C }{\partial v_{1}} \Delta v_{1} + \frac{\partial C}{\partial v_2} \Delta v_2 $$
定义$C$的梯度为偏导数的向量,$(\frac{\partial C}{\partial v_1},\frac{\partial C}{\partial v_2})^T$,定义$\Delta v \equiv (\Delta v_1,\Delta v_2)$

$$\nabla C \equiv \left( \frac{\partial C}{\partial v_1}, \frac{\partial C}{\partial v_2} \right)^T$$
则$$\Delta C \approx \nabla C · \Delta v$$
此时，假设选取
$$\Delta v = -\eta \nabla C$$
$\eta$为一个小正数(**学习速率**),则$\Delta C \approx -\eta \nabla C \cdot \nabla C = -\eta \|\nabla C\|^2$,保证了$\Delta C \leq 0$ .

算法矛盾: 
$\eta$需要足够小来使微积分方程获得更好的近似,同时如果太小的话又会导致效率过低.
在实现的过程中,$\eta$是变化的.在固定步长$\Delta v= \epsilon$ 时,$\eta = \epsilon/ \| \Delta C\|$

#### 梯度下降法神经网络

常采用随机梯度下降,通过随即选取小批量数据(m个输入)来期望其平均值大致等于整个$\nabla C$的平均值
$$ \frac{\sum_{j = 1}^{m} \nabla C_{X_j}}{m} \approx \frac{\sum_{x} \nabla C_{x}}{n} = \nabla C $$