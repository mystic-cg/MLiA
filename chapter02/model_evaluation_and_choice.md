# Concept
- 错误率:<br/>
    通常我们把分类错误的样本数占样本总数的比例称为"错误率(error rate)"<br/>
    即如果在m个样本中有a个样本分类错误,则错误率 E = a/m
---
- 精度:<br/>
    相应的, 1-a/m称为"精度(accuracy)"<br/>
    即"精度=1-错误率"
---
- 误差:<br/>
    我们把学习期的实际预测输出和样本的真实输出之间的差异称为"误差(error)"<br/>
    学习器在训练集上的误差,称为"训练误差(training error)或经验误差(empirical error)"<br/>
    在新样本上的误差,称为"泛化误差(generalization error)"
---
- 过拟合(overfitting):<br/>
    当机器学习把训练样本学得"太好"的时候<br/>
    很可能已经将训练样本自身的一些特点当作了所有潜在样本都具有的一般性质<br/>
    这样就会导致泛化性能下降
---
- 欠拟合(underfitting):<br/>
    欠拟合与过拟合相反,恰恰是学得太差了,对训练样本的一般性质未学习好
---

# P,NP,NPC,NP-Hard
    P: 能在多项式时间内解决的问题
---
    NP: 不能在多项式时间内解决或不确定能不能在多项式时间内解决,但能在多项式时间验证的问题
---
    NPC: NP完全问题,所有NP问题在多项式时间内都能约化(Reducibility)到它的NP问题,即解决了此NPC问题,所有NP问题也都得到解决
---
    NP-Hard: NP难问题,所有NP问题在多项式时间内都能约化(Reducibility)到它的问题(不一定是NP问题)
---

# Notes
    欠拟合比较容易克服,例如在决策树学习中扩展分支,在神经网络学习中增加训练轮数等
    而过拟合则很麻烦,过拟合是机器学习面临的关键障碍
    过拟合是无法彻底避免的,只能缓解
    可大致这样理解:
        机器学习面临的问题通常是NP难甚至更难,而有效的学习算法必然是在多项式时间内运行完成
        若可彻底避免过拟合,则通过惊叹误差最小化就能获最优解
        这就意味着,我们构造性地证明了"P=NP"
        因此,只要相信"P!=NP",过拟合就不可避免
---

# Data Preparation
- 留出法(hold-out)
---

- 交叉验证法(cross validation)<br/>
    k折交叉验证(k-fold cross validation),k最常用的取值是10,此时称为10折交叉验证<br/>
    ps: 10次10折交叉验证法 与 100次留出法 都是进行了100次 训练/测试<br/>
---

- 自助法(bootstrapping)<br/>
    给定包含m个样本的数据集D,对它进行采样,产生数据集D':<br/>
        每次随机从D中挑选一个样本,将其拷贝放入D',然后再将该样本放回初始数据集D中,使得该样本<br/>
        在下次采样时仍有可能被采到;这个过程重复执行m次后,我们就得到了包含m个样本的数据集D'<br/>
        - 显然,D中有一部分的样本会在D'中出现多次,而另一部分样本不出现<br/>
        - 一个简单的估计,样本在m次采样中始终不被采到的概率是$(1-\frac{1}{m})^m$<br/>
        - 取极限得到 $\lim_{m \rightarrow +\infty} (1-\frac{1}{m})^m=\frac{1}{e}\approx0.368$<br/>
        即通过自助采样,初始数据集D中约有36.8%的样本未出现在采样数据集D'中<br/>
        于是,我们将D'用作训练集,D\D'("\\"表示集合减法)用作测试集
---

#调参(parameter tuning)和最终模型
```text
    机器学习常包含两类参数:
        1.算法的参数,亦称"超参数",数目常在10以内
        2.模型的参数,数目可能很多,例如大型"深度学习"模型,甚至有上百亿个参数
    数据:
        1.train data: {training set, validation set}
        2.test data: {test set}
```

#性能度量(performance measure)<br/>
```text
    回归任务中,最常用的性能度量是"均方误差"(mean squared error)
    错误度(error rate)
    精度(accuracy)
    查准率(precision)
    查全率(recall)
    F1
    真正例(true positive; TP)
    真反例(true negative; TN)
    假正例(false positive; FP)
    假反例(false negative; FN)
        TP+TN+FP+FN=样例总数
    查准率P和查全率R分别定义为:
        P = TP / (TP + FP)
        R = TP / (TP + FN)
    ===================================
    F1是基于查准率和查全率的调和平均(harmonic mean)定义的:
        1/F1 = 0.5 * (1/P + 1/R)
        ==> F1 = 2 * P * R / (P + R) = 2 * TP / (样例总数 + TP - TN)
    F1的一般形式是Fβ,Fβ则是加权调和平均:
        1/Fβ = (1 / (1 + β*β)) * (1/P + β*β/R)
        ==> Fβ = (1 + β*β)*P*R/(β*β*P+R)
        β > 0, 度量了查全率对查准率的相对重要性
        β = 1, 即标准F1
        β > 1, 查全率有更大影响
        β < 1, 查准率有更大影响
    ROC与AUC
        ROC: Receiver Operating Characteristic(受试者工作特征)
        AUC: Area Under ROC Curve
        ROC曲线
            纵轴是真正例率(True Positive Rate, TPR)
            横轴是假正例率(False Positive Rate, FPR)
                TPR = TP/(TP+FN)
                FPR = FP/(FP+TN)
    代价敏感错误率与代价曲线
    比较校验
        假设校验
        交叉验证t校验
        McNemar校验
        Friedman校验
        Nemenyi校验
    偏差和方差
        E(f;D) = bias²(x) + var(x) + ε²
```