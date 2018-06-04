# Linear Algebra

- 矩阵可逆条件：$|A| \neq 0$。
- 奇异矩阵：方阵且$|A| \neq 0$。
- 主成分分解（PCA）：
  - 大概的思路是把一个$n\times1​$的向量$\vec x​$转换成$l\times1​$的向量$\vec c​$,本质上是找一个转换矩阵$n\times l​$的矩阵$D​$，使得$\vec x​$和$D\vec c​$尽可能相似。
  - 证明过程：
    1. 为了保证D的唯一性，要求D的每一列是单位向量，且这些列两两正交。
    2. 首先解$argmin_{\vec c} ||\vec x - D\vec c||_2$,这里最后推导出最优的$\vec c = D^T\vec x$。
    3. 然后解$argmin_D||\vec x - DD^T\vec x||_2$，这里用到了数学归纳法：
       1. 首先证明$l=1$的情况，这时候$D$变成了一个向量$\vec d$，最后推导出$argmin_d||\vec x - dd^T\vec x||_2$等价于$argmax_{\vec d}Tr(\vec dX^TX\vec d^T)$，这里只要取$X^TX$的最大特征值对应的特征向量就满足条件了。
       2. 然后数学归纳$l>1$，这时取最大的$l$个特征值对应的特征向量就行。