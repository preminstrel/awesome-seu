# 电磁场理论 Electromagnetic Field Theory

电磁场这门课是大学物理的延续，但是考的和大学物理又不太一样。教材建议用电磁场与电磁波谢处方第五版（高等教育出版社），讲的很详细很好，这本书的课后习题质量也还可以。当时我是没看网课，也没咋听课，主要就是看书+刷题。往年的题一定要刷，指导性非常强。这门课基本上也是刷题套路课，刷题量足够了分数也就上去了，期末 90+ 不算难。

下面给出一些容易错的地方：

- 两个不同频率的量不可以用复数表示
- 传播方向不同的电磁波不能用 $H=\frac{1}{\eta} \vec{n}\times \vec{E}$ 来计算，因为方向是不固定的
- $$\nabla \times \nabla \times \vec{A}=\nabla (\nabla \cdot \vec{A})-\nabla^2\vec{A}$$
- 电流连续性方程 （电荷守恒方程组）：单位流出曲面的电流等于其包围的体积内电荷的减少量，它是建立在什么基础上的？$$\nabla \cdot \vec{J}=-\frac{\partial \rho}{\partial t},\qquad \oint_S\vec{J}d\vec{S}=-\int_V \frac{\partial \rho}{\partial t}dv $$
- 混合模
- 复矢量形式用$\vec{A}$ 和 $\varphi$ 表示电场强度和磁感应强度
- 如何求单位长度的电感
- 矢量位的洛伦茨规范 $\nabla \cdot \vec{A}+\mu \varepsilon \frac{d\varphi}{dt}=0$，推导标量位 $\varphi$ 所满足的波动方程（利用 $\vec{E}=-\nabla \varphi - \frac{\partial \vec{A}}{\partial t}$）$$\nabla^2\varphi-\mu\varepsilon\frac{\partial^2 \varphi}{\partial t^2}=-\frac{\rho}{\varepsilon}$$
- **坡印亭矢量 $\vec{S}=\vec{E}\times \vec{H}$ 的物理意义**：在闭合曲面上的面积分等于从该闭合曲面所包围体积中散发出去的功率，任何瞬间流入某闭合曲面的功率等于从闭合曲面所包围体积内电场和磁场所存储的能量的增加率与欧姆损耗功率之和
- 关于极化：注意利用 $\varphi = \frac{E_x}{E_y}>0$ 判断右旋，则要求 $\vec{x}\times \vec{y}=\vec{z}$ ，要求传播方向和其满足对应的右手螺旋关系——分解正交系
- 能够建立二维静态场的导波系统能传输TEM波
- 分清波数 $\vec{k}$，相位常数 $\beta$，截止波数 $\gamma$
- 可以推导矢量磁位和标量电位所满足的非齐次波动方程、会推导电场/磁场的波动方程
- 当给出的电场为驻波的时候的时候，不可以用均匀平面波的公式 $\vec{H}=\frac{1}{\eta}\vec{k_0}\times \vec{E}$ 直接求解
- 不要忘了波阻抗最基本的定义 $\eta = \frac{|E|}{|H|}$ 常用来求相对介电常数（利用本征为 $120\pi$）; 同时 $\vec{k_0}=\frac{\vec{E_0}\times \vec{H_0}}{|E_0||H_0|}$；别忘了均匀平面波的 $\vec{k}\cdot \vec{H}=0$
- 电偶极子远区条件，等相位面，电场磁场空间垂直，时间相位相等
- 泊松方程后面是不等于0的，Laplace方程后面是等于0的
- 写题目的时候记得加上矢量符号
- 色散、群速度、相速度定义
- 电偶极子
- 近区场性质，远区场与均匀平面波的异同
- 各个物理量的单位
- Maxwell 式对应的物理定律

- 法拉第电磁感应定律：感应电动势等于磁通变化率的负值 $$\varepsilon=-\frac{d\phi}{dt}=-\frac{d}{dt}\iint\vec{B}\cdot d\vec{S}=-\iint\frac{\partial \vec{B}}{\partial t}\vec \cdot d{S}+\oint\vec{v}\times \vec{B}\cdot d\vec{l}$$
- 正交坐标系掌握
- 传导电流 $I_c$ + 运流电流 $I_v$ + 位移电流 $I_d$ = 全电流
- 电位的边界条件
- $J=\rho_S v\quad J=Nqv$
- 恒定电流场的基本方程
- 拉普拉斯算符 $\nabla^{2}$

$$
\begin{gathered}
\nabla^{2}=\nabla \cdot \nabla=\frac{\partial^{2}}{\partial x^{2}}+\frac{\partial^{2}}{\partial y^{2}}+\frac{\partial^{2}}{\partial z^{2}} \\
\nabla^{2} V=\nabla \cdot(\nabla V)
\end{gathered}
$$

- 几个矢量运算恒等式

$$
\begin{gathered}
\nabla \times(\nabla \times A)=\nabla(\nabla \cdot A)-\nabla^{2} A \\
\nabla \cdot(A \times B)=B \cdot(\nabla \times A)-A \cdot(\nabla \times B) \\
\nabla \cdot(\phi A)=(\nabla \phi) \cdot A+\phi(\nabla \cdot A) \\
\nabla \times(\phi A)=(\nabla \phi) \times A+\phi(\nabla \times A)
\end{gathered}
$$
- 矢量三重积 $$A\times (B\times C)=B(A\cdot C)-C(A\cdot B)$$
