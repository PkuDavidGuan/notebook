# AlphaGo Zero

1. self play：每一步都是站在当前player的立场上，选择一个胜率最大的动作。

   1. 蒙特卡洛搜索树（MCTS）
      - edge：$(s,a)$。$s$代表当前棋局的状态，$a$代表可能选择的动作
      - UCB公式（upper confidence bound）$v_i+C*\sqrt{\frac{logN}{n_i}}$。其中$v_i$是节点估计的值，$n_i$是节点被访问的次数，而$N$则是其父节点已经被访问的总次数。$C$是可调整参数。
        - $n_i$在分母上的原因是为了探索更多新的节点。举例来说，假如当前节点是$A$，$A$有4个子节点$A_1,A_2,A_3,A_4$,节点$A_1$的UCB值很大，那么每次运行到节点$A$时，第一次会选择$A_1$,但随着访问次数的增多，$A_1$的UCB值渐渐减小，使得其他子节点也有机会被访问。
      - 流程：（123迭代进行）
        1. 选择(select)：从根节点开始，在选择阶段，需要从根节点，向下选择出一个最急迫需要被拓展的节点N。具体流程是：判断该节点的所有动作是否都被扩展过，如果是，则移动到UCB值最大的子节点，继续选择；如果不是，则选择该节点。
        2. 拓展(expand)：随机选择节点N的一个未被扩展过的子节点Nn。
        3. 模拟(simulation)：模拟Nn之后的情景。Marto Carto体现在这一步。

2. neural network construction

   1. input：$s$；output：$(\vec p,v)$，$\vec p$代表走每个动作的概率，$v$代表当前player胜利的概率。
   2. 训练集：self-play的每一步
   3. 网络架构：resnet，由于网络很深，可能产生梯度变成零的问题，于是使用了resnet：

   ![resnet](/Users/DavidGuan/Desktop/notebook/fig/resnet.png)

3. AlphaGo Zero的训练过程就是第1、2步的迭代，第1步的MCTS是用上一轮的神经网络做决策，第2步的神经网络是用本轮self-play的数据做训练集。