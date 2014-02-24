统计学习导论-非线性
========================================================

# 多项式回归

- 模型基本形式为单一自变量在不同幂指数下的多项式，最小二乘拟合
- 模型在特定点的方差受系数方差与协方差影响，幂越高，模型越精细，方差越大
- 幂次一般不超过3或4
- 可进行logistic回归

# 阶梯函数

- 阶梯函数将自变量由连续变成有序分类变量
- 函数形式为引入指标函数$C_K(x)$进行自变量分段，然后进行最小二乘拟合
- 依赖找间隔点
- 可进行logistic回归

# 基函数

- 固定线性系数$\beta$,自变量的形式由$b(x)$决定，$b(x)$为基函数
- 多项式回归与阶梯函数均为基函数的特例

# 回归样条

- 设定分段点，分段点前后进行多项式回归
- K个点分割(K+1)段，存在(K+1)个多项式回归，自由度过高
- 进行边界约束，对n次方程而言，约束分段点0阶，1阶，2阶导数连续，减少3个自由度，共有K个点，则有$(n+1-3)k + n + 1$个自由度，相比无约束的$(n+1)k$，自由度减少，更稳健
- 一般而言约束限制为(自由度-1)阶连续，这样自由度比分界点略多些，够用
- 分段样条最好在两端加入线性限制，收敛自由度，这样在边界稳健，为自然样条
- 分段点位置一般均匀分布，个数（本质上是自由度）通过交叉检验来确定
- 分段多项式回归限定了自由度，因此结果一般比多项式回归更稳定

# 平滑样条

- 如果以RSS衡量不加入限制，很容易产生过拟合，因此考虑加入平滑项
- 最小化 $$ \sum_{i = 1}^n (y_{i} - g(x_i))^2 + \lambda \int g''(t)^2 dt $$ 其中，$g(x)$为平滑样条，由损失函数与惩罚项组成，二次导数表示在t处的平坦度，越平坦，惩罚越小，越崎岖，惩罚越大，因而平滑
- 对三次函数而言，平滑样条会将函数两端收敛的跟自然样条一样，实际上，平滑样条是自然样条的收缩版
- 参数$\lambda$也影响平滑效果，越大越平滑，因为k固定，只涉及$\lambda$的选择
- 参数$\lambda$的选择基于有效自由度，可以用留一法进行估计，形式与杠杆点统计量差不多，可以很方便的进行数值求解
- 平滑样条的自由度比多项式要小，更稳健

# 本地回归

- 首先分段，然后分段内进行加权回归，离某点越近，权重越高，进行最小二乘拟合，得到每个点的函数，联合模型拟合
- 自变量较多，可考虑本地有选择的选取自变量进行本地回归
- 同样遭受高维诅咒带来的临近值少或稀疏问题

# 广义加性模型

- $$y_i = \beta_0 + \sum_{i = 1}^n f_j(x_{ij}) + \epsilon$$ 每个自变量都有自己的函数形式，加合求解
- 每个自变量影响都可以展示
- 可分段，也可使用平滑，平滑方法中使用了反馈拟合策略对不易用最小二乘拟合求解的问题进行求解，效果差不多，分段不必要
- 可用于分类回归问题，解释性好
- 优点：非线性，更准确，易解释，可进行统计推断，可用自由度衡量平滑性
- 缺点：不易考虑交互影响

