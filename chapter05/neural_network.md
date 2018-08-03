# Neural Network
## 神经元模型
        神经网络是由具有适应性的简单单元组成的广泛并行互连的网络, 它的组织能够
    模拟生物神经系统对真实世界物体所作出的交互反应

        神经网络中最基本的成分是神经元(neuron)模型, 即上述定义中的"简单单元".
    在生物神经网络中, 每个神经元与其它神经元相连, 当它"兴奋"时, 就会向相连的
    神经元发送化学物质, 从而改变这些神经元内的电位; 如果某神经元的点位超过了一个
    "阈值"(threshold), 那么它就会被激活, 即"兴奋"起来, 向其它神经元发送化学物
    质
[![M-P Neuron Model](https://i.loli.net/2018/07/22/5b5481fb7dfcd.jpg)](https://i.loli.net/2018/07/22/5b5481fb7dfcd.jpg)
## 感知机(Perception)与多层网络
    感知机由两层神经元组成, 输入层接收外界输入信号后传递给输出层, 输出层是M-P神经元, 亦称
    "阈值逻辑单元"(threshold logic unit)
    感知机只有输出层神经元进行激活函数处理, 即只拥有一层功能神经元(functional neuron),
    其学习能力有限.
    若两类模式是线性可分的, 即存在一个线性超平面能将它们分开;
    则感知机的学习过程一定会收敛(converge), 而求得适当的权向量W=(w1;w2;...;wn+1);
    否则, 感知机学习过程将会发生振荡(fluctuation), W难以稳定下来, 不能求得合适解
    多层功能神经元, 可以解决非线性可分问题
- 多层前馈神经网络(multi-layer feed-forward neural network)<br/>
每层神经元与下一层神经元全互连, 神经元之间不存在同层连接, 也不存在跨层连接
## 误差逆传播算法(error BackPropagation)
    BP是基于梯度下降(gradient descent)策略, 以目标的负梯度方向对参数进行调整.
## 全局最小(global minimum)和局部最小(local minimum)
    跳出"局部最小"的策略
- 使用随机梯度下降
- 使用模拟退火(simulated annealing)
- 以多组不同参数值初始化多个神经网络, 按标准方法训练后, 取其中误差最小的解作为最终参数
- 使用遗传算法(genetic algorithms)
## 其他常见神经网络
- RBF(Radial Basis Function, 径向基函数)网络<br/>
    一种单隐层前馈神经网络, 它使用径向基函数作为隐层神经元激活函数, <br/>
    而输出层则是对隐层神经元输出的线性组合
- ART(Adaptive Resonance Theory, 自适应谐振理论)网络<br/>
- SOM(Self-Organizing Map, 自组织映射)网络<br/>
- 级联相关(Cascade-Correlation)网络<br/>
- Elman网络<br/>
- Boltzmann机<br/>


