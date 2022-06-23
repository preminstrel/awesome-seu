# VLSI 基础

教材用的是 Rabaey 的《数字集成电路——电路、系统与设计（第二版）》。这本书被称为数字电路的圣经，写的也很有条理，但是第一次看可能会比较晦涩难懂。由于笔者在学 VLSI 基础之前学过数字集成电路的必修课，很多内容都是重叠的，故学起来略微轻松一些。这里给出了笔者认为一些容易忽略的点（不一定是重要的，特别基础的也不一定包括在内）。

**以后希望在数字 IC 方向发展的同学这门课请务必好好学。**

## Chapter 1: Introduction
- 芯片成本正比于面积的四次方 $S^4$
- $V_{IL}, V_{IH}$ 定义为 VTC 增益为 -1 的点，之间的区域称为不确定区，也叫过渡宽度（Transition Width, TW）
- $NM_L=V_{IL}-V_{OL}, NM_H=V_{OH}-V_{IH}$
- 再生性保证了一个受干扰地信号在通过若干逻辑级后逐渐收敛回到额定电平中的一个（要具有再生性，需要 VTC 有一个增益大于 1 的过渡区）
- 理想：负载门的 $R_{in}$ 尽量大（输入电流最小），驱动门的 $R_{out}$ 尽量小（减小负载电流对输出电压的影响）
- $t_p$ 定义了它对输入信号变化的响应有多快，定义为输入和输出波形 50% 翻转点之间的时间。**$t_r$: rise time;  $t_f$: fall time 是用来衡量单个信号波形而不是门的，表明了信号在不同电平间翻转有多快**

$$
t_p=\frac{t_{pLH}+t_{pHL}}{2}
$$
- 环振：$T=2Nt_p>>t_f+t_r$
- 一阶 RC 电路 $v_{out}=(1-e^{-t/\tau})V$ $0.69 \tau$ : 0~50%， $2.2\tau$ : 10%~90%
- 峰值功耗 $P_{peak}=i_{peak}V_{supply}$，平均功耗 $P_{av}=\frac{1}{T}\int_t^{t+T}p(t)dt=\frac{V_{supply}}{T}\int_t^{T+t}i(t)dt$
- Power-Delay Product (PDP): $E=P_{av}\times t_p$ ; Energy-Delay Product (EDP): $E\times t_p$

## Chapter 3: Devices
### PN Junction
- 二极管内建电势 $\Phi_0=\Phi_T\ln(\frac{N_AN_D}{n_i^2})$ 其中 $\Phi_T=\frac{kT}{q}=26mV$ 
- 理想二极管模型：$I_D=I_S(e^{V_D/\Phi_T}-1)$； 一阶二极管模型：$V_{Don}=0.7V$
- 实际器件中反向电流大大超过饱和电流 $I_S$，这是由于在耗尽区因热而产生电子空穴对所造成的
- 二极管结电容：$C_j=\frac{C_{j0}}{(1-V_D/\Phi_0)^m}$，$C_{j0}$ 是零偏下的电容，$m$ 是梯度系数，突变为 0.5，线性为 0.33 **此处有结电容与外加偏置电压的关系图 P55**
- 二阶效应：强电场产生高速载流子，激发电子空穴对（雪崩击穿）
- 二极管的 SPICE 模型（P57）
### MOSFET
- MOSFET：性能好，寄生效应小
#### Static
- 阈值电压 $V_T$：发生强反型时的 $V_{GS}$；$\gamma$ 为体效应系数 
$$
V_T=V_{T0}+\gamma(\sqrt{|-2\phi_F+V_{SB}|}-\sqrt{|-2\phi_F|})
$$
- $C_{ox}=\frac{\varepsilon_{ox}}{t_{ox}}$ 为栅氧的单位面积电容
- 沟道长度调制效应：$L\to L-\Delta L$，沟道变短了，会发生隧穿，电子走的更容易了（短沟道显著）
- 速度饱和：当沿沟道电场达到某一临界值 $\xi_c$ 的时候，载流子的速度将由于散射效应而趋于饱和（PMOS 中速度饱和效应不太显著）
- MOS 管模型：（其中 $V_{\min}=\min(V_{GT},V_{DS},V_{DSAT})$）
$$
I_D=k'\frac{W}{L}(V_{GT}V_{\min}-\frac{V_{\min}^2}{2})(1+\lambda V_{DS})
$$
- 等效电阻 $R_{eq}$ 反比于器件宽长比 $\frac{W}{L}$，$V_{DD}\gg V_T+V_{DSAT}/2$ 时与 $V_{DD}$ 几乎无关，$V_{DD}$ 接近 $V_T$ 时电阻急剧提高
- 传播延时：$0.69R_{on}C_L, V_{DS}=V_{DD}/2$ ($V_M$ 点)，计算 $V_{DD}\to V_{DD}/2$ 的等效电阻 
$$
R_{eq}=\frac{3}{4}\frac{V_{DD}}{I_{DSAT}}(1-\frac{7}{9}\lambda V_{DD})
$$
#### Dynamic
- 电容包括本征寄生电容、互连线寄生电容、负载电容。
- 覆盖电容：$C_{GSO}=C_{GDO}=C_{ox}x_dW=C_oW \quad (C_{gate}=C_{ox}WL)$

| 工作区域 | $C_{GCB}$  | $C_{GCS}$             | $C_{GCD}$             | $C_{GC}$              | $C_G$                       |
| -------- | ---------- | --------------------- | --------------------- | --------------------- | --------------------------- |
| 截止区   | $C_{ox}WL$ | 0                     | 0                     | $C_{ox}WL$            | $C_{ox}WL+2C_oW$            |
| 电阻区   | 0          | $\frac{1}{2}C_{ox}WL$ | $\frac{1}{2}C_{ox}WL$ | $C_{ox}WL$            | $C_{ox}WL+2C_oW$            |
| 饱和区   | 0          | $\frac{2}{3}C_{ox}WL$ | 0                     | $\frac{2}{3}C_{ox}WL$ | $\frac{2}{3}C_{ox}WL+2C_oW$ |
- 当 $V_{GS}$ 开始增大时候，在栅下形成了一个耗尽区，使栅的绝缘层加厚 ($t_{ox}\uparrow$)，电容会暂时减小，**具体见 P73 图**
- 结电容是由反向偏置的源-体和漏-体之间的 PN 结引起的，由底板 PN 结和侧壁 PN 结组成。
$$
C_{diff}=C_{bottom}+C_{sw}=C_jL_SW+C_{jsw}(2L_S+W)
$$

#### SEcondary effect
- $L\downarrow$ 导致 PN 结耗尽区占比增大，进一步导致阈值电压 $V_T$ 的降低
- 短沟道时，通过增大 $V_{DS}$，进一步导致阈值电压 $V_T$ 的降低
- 亚阈值情况（弱反型）、寄生电阻\*、闩锁效应\*

## Chapter 4: Wire
- 导线的平行板电容模型 $C_{int}=\frac{\varepsilon_{di}}{t_{di}}WL$，考虑边缘场，得到 **（图片见 P94）**

$$
c_{wire}=c_{cpp}+c_{fringe}=\frac{w\varepsilon_{di}}{t_{di}}+\frac{2\pi \varepsilon_{di}}{\log(2t_{di}/H+1)}
$$

- 接地电容+导线间电容 **（图片见 P95）**
- 电阻 $R=\frac{\rho L}{A}=\frac{\rho L}{HW}$，方块电阻可以定义为 $R_{\blacksquare}=\frac{\rho}{H}$
- 接触电阻：布线层之间的转接产生的电阻（0.25um工艺时，金属至多晶5～20Ω，金属层间1～5 Ω ）
- 趋肤效应：高频电流趋向导体的表面流动，使导体电阻随频率提高而增加。GHz信号线设计需要特别考虑（如时钟线）
- 集总模型：导线电阻很小时，相当于仅增加负载电容。$\tau=RC, t_p=0.69RC, t_r=2.2RC$
- 分布 $rc$ 线模型：$\tau=RC\frac{N+1}{2N}=\frac{RC}{2}=\frac{rcL^2}{2}, t_p=0.38RC, t_r=0.9RC$
- 内阻为 $R_s$ 的电源驱动长度为 $L$ 的 $rc$ 线 
$$
\tau_D=R_sC_w+\frac{R_wC_w}{2}=R_sC_w+0.5r_wc_wL^2, \quad t_p=0.69R_sC_w+0.38R_wC_w
$$
- $rc$ delays should only be considered when $t_{pRC} > t_{pgate}$ of the driving gate ，可以计算导线的临界长度
$$
L_{crit}=\sqrt{\frac{t_{pgate}}{0.38rc}}
$$
- $rc$ delays should only be considered when the rise (fall) time at the line input is smaller than RC, the rise (fall) time of the line （输入信号要足够快）
$$
t_{rise}<RC
$$

## Chapter 5: The Inverter
- $t_p=0.69R_{on}C_L$，所以一个快速门的设计是通过减小输出电容或者减小晶体管的导通电阻实现的
### Static
- 开关阈值 $V_m\approx \frac{rV_{DD}}{1+r}$ ，其中 
$$
k_nV_{DSATn}(V_M-V_{Tn}-\frac{V_{DSATn}}{2})+k_pD_{DSATp}(V_M-V_{DD}-V_{Tp}-\frac{V_{DSATp}}{2})=0
$$
$$
V_M=\frac{(V_{Tn}+\frac{V_{DSATn}}{2})+r(V_{DD}+V_{Tp}+\frac{V_{DSATp}}{2})}{1+r},\quad r=\frac{k_pV_{DSATp}}{k_nV_{DSATn}}=\frac{v_{satp}W_p}{v_{satn}W_n}
$$
- $g$ 随着 $V_M$ 变小而变大，但是噪声容限绝对值变小，相对值变大
- 降低电源电压可以改善增益，过低的工作电压，将加大延时；加大 DC 特性对器件参数（如VT）的敏感度；对外部噪声敏感
- 对非常低的工作电压来说，传输特性会很差（电源低于阈值电压，工作在亚阈值区域）
### Dynamic
- 计算电容值：栅漏电容为 $C_{gd12}=2G_{GDO}W$，扩散电容 $C_{db1},C_{db2}$，连线电容 $C_w$，扇出的栅电容 $C_{g3},C_{g4}$
- 过冲：反相器晶体管的栅漏电容造成的，它们在晶体管对输入变化开始响应之前就直接把输出节点上变化陡峭的阶跃电压耦合到输出上。
- $t_p\approx 0.52\frac{C_L}{(W/L)_nk_n'D_{DSATn}}$，和 $V_{DD}$ 基本无关，由于沟道长度调制效应，增加 $V_{DD}$ 会降低延时；当 $V_{DD}$ 接近 $2V_T$ 时，延时会迅速增加（沟道层变窄，电阻变大）
- 以对称性（$\beta=2.4, t_{pHL}=t_{pLH}$）和噪声容限为代价，较小的器件尺寸得到了较快的面积（$\beta=1.9$）
- 尺寸变大导致电流增加的同时输出电容也在增加，引发自载效应，存在本征延时 $t_{p0}$ ，本征电容 $C_{int}$ 包括扩散电容和密勒电容（都正比于晶体管的宽度），$C_{int}=SC_{iref}$，$R_{eq}=R_{ref}/S$，反相器的本征延时与门的尺寸无关，仅取决于工艺/反相器的版图

$$
t_p=0.69R_{eq}(C_{int}+C_{ext})=t_{p0}(1+C_{ext}/C_{int})
$$

$$
R_w=R_{unit}/W,\quad C_{int}=WC_{unit},\quad t_{p0}=0.69R_{unit}C_{unit}
$$

$$
t_{p0}\propto \frac{V_{DD}}{V_{DD}-V_T-V_{DSAT}/2}
$$
- 输入栅电容和本征输出电容之间的关系 $C_{int}=\gamma G_g$ ，等效扇出 $f$ 指的是外部负载电容和输入电容之间的比值
$$
t_p=t_{p0}(1+\frac{C_{ext}}{\gamma C_g})=t_{p0}(1+\frac{f}{\gamma})
$$

- 确定反相器链的尺寸：$C_{g,j}=\sqrt{C_{g,j-1}C_{g,j+1}}$，每个反相器的尺寸都相对于前面尺寸放大 $f$ 倍（$1,f,f^2,f^3\cdots,f^N=F=C_L/C_{g,1}$），即每个反相器都有相同的等效扇出 $f_i=f=\sqrt[N]{F}$ 
$$
t_p=Nt_{p0}(1+f/\gamma)
$$
- 确定反相器链的级数：$f=e^{1+\gamma/f}$，$\gamma=0,N=1;\gamma=1,N=3.6$
- 修正表达式 $t_p^i=t_{step}^i+\eta t_{step}^{i-1}$
### Power Dissipation
- 如果某个门每秒通断 $f_{0\to 1}$ 次，则功耗为
$$
P_{dyn}=C_LV_{DD}^2f_{0\to 1}
$$
- 通过一个传输管来降低摆幅，从而降低能耗 $E_{0\to 1}=C_LV_{DD}(V_{DD}-V_T)$
- 对于直接通路电流引起的功耗来说，输入变化要求快速，这样不容易形成直流通路 
$$
\frac{t_{in}}{t_{out}}\propto P_{dp}
$$
- 降低电源电压时，短路电流的影响减小，如果 $V_{DD}<V_{Tn}+|V_{Tp}|$ 的时候，短路功耗将被消除，因为两个器件绝不会同时导通
- 能量最优点要小于性能最优点

## Chapter 6: Combinational Logic Circuits
### Static CMOS
- 上拉管和下拉管的能力决定了 $V_M$ 的大小，而不是传播延时
- 传播延时和输出节点附近的 NMOS 管是否导通有关，因为存在 $C_{int}$，若导通，延时会大
- 调整 MOS 面积大小时，可以适当调大公用的 MOS 管来降低总面积
- Fan In：晶体管个数很多增加了该门的总电容，本征电容随扇入线性增加，**$t_{pHL}$ 呈平方关系，$t_{PLH}$呈线性关系**。所以扇入应该避免大于等于 4 的情况
$$
t_{pHL}=0.69R_N(C_1+2C_2+\cdots+NC_L)\propto N^2
$$
- Fan-out: each additional fan-out gate adds two gate capacitances ($C_{gPMOS}$ & $C_{gNMOS}$) to $C_L$：$t_p=a_1FI+a_2FI^2+a_3FO$
- 大 Fan In 时的设计技术：调整晶体管尺寸、逐级加大晶体管尺寸（最下面的最大，因为出现次数多）、重新安排输入--把关键路径放在输出处（下面的电容先放电好了）、重组逻辑结构、插入反相器（buffer）来隔离 Fan In 和大电容的 Fan Out、降低电压摆幅（但是会导致后一级门慢，可以用灵敏放大器恢复摆幅）
#### Delay in a Logic Gate
$$
t_p=t_{p0}(p+gf/\gamma)
$$
- $t_{p0}$ 代表反相器的本征延时
- $f$ 为等效扇出/电气努力（外部负载和输入电容之间的比）
- $p$ 代表该门与简单反相器的本征延时之比（与门的拓扑结构/版图样式有关），$n$ 输入的 NAND、NOR 为 $n$，$n$ 路多路开关为 $2n$，XOR/NXOR 为 $n2^{n-1}$
- $g$ 是逻辑努力，代表一个门和反相器提供相同电流的情况下它的输出电容要比反相器大多少，个人感觉就是输出端的一个 PMOS 和 NMOS 电容相加；NAND 为 $(n+2)/3$，NOR 为 $(2n+1)/3$；Multiplexer 为 2，XOR 为 4（input=2）/12（input=3）
- 门努力 $h=gf$
- Gate delay: $d=gf+h$
- 分支努力 $$b=\frac{C_{on-path}+C_{off-path}}{C_{on-path}}$$
- 最优化的时候每一级的门努力相同：$f_1g_1=f_2g_2=\cdots =f_Ng_N$
- 路径逻辑努力 $G=\prod_1^N g_i$
- 路径有效扇出 $F=\frac{C_L}{C_{g1}}=\prod_1^N\frac{f_i}{b_i}=\prod f_i/B$
- 路径分支努力 $B=\prod_1^N b_i$
- 总路径努力 $H=\prod_1^N h_i=\prod_1^N g_if_i=GFB$
##### Optimum Effort per Stage
使路径延时最小的门努力为 $$h=\sqrt[N]{H}$$ 此时通过路径的最小延时为 
$$
D=t_{p0}\left(\sum_{1}^N p_i+\frac{N(\sqrt[N]{H})}{\gamma}\right)
$$
##### Optimal Number of Stages
通常不考虑，因为组合逻辑的级数由功能决定

##### Method of Logical Effort
- 计算路径努力 $H=GFB$
- 计算使路径延时最小的门努力 $h=\sqrt[N]{H}=g_if_i$
- 求各级的参数 $C_{out}=C_{in}*f=C_{in}*h/g$
- 各级尺寸 
$$
s_i=\left(\frac{g_1s_1}{g_i}\right)\prod_{j=1}^{i-1}\left(\frac{f_j}{b_j}\right)
$$

#### Ratioed Logic
- 一个较大的 PMOS 上拉器件不仅提高了性能，同时也由于增加了 $V_{OL}$ 而使静态功耗增加和噪声容限减小
- 优化：Adaptive Load（上面并联了一个大尺寸 PMOS $\overline{Enable}$ 驱动）、DCVSL
- DCVSL：输入正反逻辑，两条路----修正摆幅、消除静态功耗、同时得到正负逻辑、但是需要反向逻辑的输入、面积比静态 CMOS 要小（因为都是 NMOS）、有瞬间的导通电流、导线数量加倍电路复杂动态功耗较高

#### Pass-Transistor Logic
- 注意输出不要出现三态情况
- 管子数目少、结构规则易优化
- 如果下一级连了 CMOS，因为阈值损失会导致产生静态电流（短路电流），引起静态功耗；同时也会导致 NMOS 的导通电阻增大，进一步影响延时-----> 功耗性能双劣化
- 差分传输管逻辑、差分摆幅恢复传输管逻辑（门与门之间要插入缓冲器，否则会有竞争）
##### 电平恢复
- 优点：全摆幅
- 缺点：增加复杂性（有比电路）、晶体管尺寸考虑（有可能恢复管太强）、增加了内部节点 X 上的电容从而减慢了这个门的速度
##### 多种阈值晶体管
- 优点：用低阈值电压的 NMOS 管可以消除大部分阈值损失，不会使下一级的 PMOS 导通，可以传输比较高的高电平
- 缺点：对功耗有负面影响，由于 $V_{GS}<V_T$，会有亚阈值电流流过传输管使得功耗的产生（NMOS 管的 $V_T$ 越低亚阈值电流越大）；无法实现真正的 $V_{DD}$ 传输（有体效应）
##### 传输门
- 缺点：需要有 PMOS 和反逻辑输入
- 传输门的电阻 $R_{eq}$ 几乎不变，可以用一个常数值代替
- 2-1 MUX、XOR **(P185)**
- 传输门链的延时（与 $n^2$ 成正比） $$t_p=0.69CR_{eq}\frac{n(n+1)}{2}$$
- 每隔 $m$ 个传输门插入一个 Buffer，可以得到延时（与 $n$ 成正比）
$$
t_p=0.69\left[CR_{eq}\frac{n(m+1)}{2}\right]+(\frac{n}{m}-1)t_{buffer}
$$
$$
m_{opt}=1.7\sqrt{\frac{t_{buffer}}{CR_{eq}}}\qquad \text{目前典型值为 3 或 4}
$$
### Dynamic Logic
N+2 个晶体管，避免伪 NMOS 的静态功耗，没有短路电流，输出可能是高阻态，全摆幅，无比逻辑（器件的尺寸不影响电平），更快的切换速度
$$
Out=\overline{CLK}+F\cdot CLK
$$

缺点：高动态功耗，低噪声容限，需要预充电时钟，要给时钟信号负载
- 也可以用 PMOS 来实现，但是 PMOS 比 NMOS 慢，因为 PMOS 管的驱动电流较小
- 问题 1 - 电荷泄漏：存在漏电流（反偏二极管和亚阈值漏电）会让电荷逐渐漏掉，因此会有一个最低的时钟频率要求；**解决方法：增加一个泄漏晶体管（伪 NMOS 上拉器件或者输出接反相器再作为一个 PMOS 上拉管的输入 [反馈形式]）**
- 问题 2 - 电荷分享：下拉网络的一个电容被充电，$C_L\to C_L+C_A$，进一步导致输出电平的下降 
$$
\Delta V_{out}=-\frac{C_A}{C_L}(V_{DD}-V_{Tn}(V_X))\qquad if \quad\Delta V_{out}<V_{Tn}$$$$\Delta V_{out}=-V_{DD}(\frac{C_A}{C_L+C_A})\qquad if \quad\Delta V_{out}>V_{Tn}
$$ 
**解决办法：对那个电荷分享的节点进行电平补偿（预充电），但是会增加面积和电容/功耗**
- 问题 3 - 背栅耦合：输出节点的高阻抗会让电路对串扰的影响十分敏感，输出的变化会通过栅源和栅漏电容耦合到之前的输出（即输出至输入的耦合）
- 问题 4 - 时钟馈通：相当于过冲，由预充电器件的时钟输入和动态输出节点之间的电容耦合引起的效应。耦合电容由预充电器件的栅漏电容组成，包括了覆盖电容和沟道电容。
- 两个动态逻辑不可以直接串联，前一级要放电要时间，会使得后一级输出错误！可以用多米诺逻辑，在两者之间加一个反相器（输入端仅接受 0-1 的转变，非反相逻辑），可以实现非常高的速度。**扇出是一个巨有低阻抗输出的静态反相器驱动，提高了抗噪声能力；同时由于缓冲器隔离了内部和负载电容，减少了动态输出节点的电容。**
- 可以把多米诺逻辑的 NMOS 求值管给去掉，不存在输出高电平会下降的情况，但是有可能因为延时会产生短路电流
- 差分多米诺逻辑：解决了非反向逻辑的问题
- np-CMOS：CLK 相反，省去了反相器；但是 PMOS 模块要比 NMOS 慢，所以需要额外的面积，由于缺少 Buffer，所以存在与动态节点之间的连线。

## Chapter 7: Sequential Logic Circuits
### Static Latch and Register
- $t_{su}$：建立时间，CLK 来之前的时间；$t_{hold}$：保持时间，CLK 来之后的时间；$t_{c-q}$：传播延时，Q 端输出的延迟
- 最小时钟周期：$T\ge t_{c-q}+t_{plogic}+t_{su},\quad  t_{cdregister}+t_{cdlogic}\ge t_{hold}$
- 伪静态：根据时钟的不同状态，寄存器采取了静态或动态的存储方式，太长时间间隔会导致漏电破坏状态
- 产生两不重叠时钟的电路（P224）
- SR 触发器的 Set up 时间和 Hold 时间与 $t_{c-q}$ 的关系
### Dynamic Latch and Register
- 动态边沿触发寄存器：$t_{su}=t_{T1}, t_{c-q}=t_{T2}+2t_{inv}$
- 时钟重叠是一个重要的问题，可以通过保证输入和输出有足够的延时来解决
- $C^2MOS$ 因为具有 $CLK,\overline{CLK}$ 时钟控制的，所以对时钟重叠是不敏感的（信号传播需要在一个上拉之后跟着一个下拉，或反过来亦可--相邻的两个 part 是时钟相反的）；但是一旦重叠结束就会导通，所以要求数据应该在重叠期保持稳定
- TSPCR 真单相钟控寄存器仅用单相位时钟，缺点是稍微增加了晶体管的数目（12个）；如果输出节点连接传输门有可能发生电荷分享，动态节点应该借助静态反相器隔离或者设计成伪静态提高抗噪能力
- TSPC 可以实现将逻辑功能嵌入电路中 
- TSPC Latch 可以简化成只有一个 CLK 输入，时钟负载减半，但是无法让所有节点达到全摆幅（P233）
- TSPC 可以中间插入一个动态反相器实现寄存器功能（缺点：需要 $t_{hold}$）
- $$
t_{su}=t_{inv}\qquad t_{c-q}=3t_{inv}
$$

- 脉冲寄存器：只在很短的窗口内采样输入，所以透明时间很短，避免了竞争情况
- 短脉冲产生器
- 如何增加使能输入？
- 流水线：在各计算单元中插入寄存器，省去时间（不断有数据进来的前提下）
### 非双稳时序电路
- 滞环特性：开关阈值是可变的且取决于翻转的方向，可以把一个含噪声或缓慢变化的输入信号转变成一个干净的输出信号，利用了正反馈
- 单稳时序电路：只有一个稳态（它的静态），经过一个触发后过一段时间后回到稳态 - 单脉冲电路（延时+XOR）
- 差分电路的振荡电路*

## Chapter 9: Coping with Interconnect
降低鲁棒性、增加延时、增加能耗
### Capacitance
- 串扰：由相邻的信号线与电路节点之间耦合引起的干扰，希望受害线的驱动阻抗降低来降低 $\tau_{XY}=R_Y(C_{XY}+C_Y)$，希望上升时间要近似或大于时间常数（干扰的峰值会减小）
- 克服电容串扰方法：
	- 避免浮空节点
	- 敏感节点应当很好地与全摆幅隔离
	- 增加上升降低时间（但是会对短路功耗有影响）
	- 采用差分信号传输方法（使串扰信号变为不会影响电路的共模噪声源）
	- 不要使两条信号线之间电容太大（很长的平行导线）
	- 在两个信号之间增加一条屏蔽线（$V_{DD}$ 或 $GND$，使得变成接地电容）
	- 增加额外的布线层，每一个信号层都用一个 $V_{DD}$ 或 $GND$ 金属平面相间隔
- 密勒效应：动态过程中电容会翻倍
- 串扰对性能的影响（$R_D$ 为驱动器的等效电阻）：$$t_{p,k}=gC_w(0.38R_W+0.69R_D)$$
- 最小宽度的导线先以最小节距不限，相邻层的导线相互垂直布线，使串扰最小。缺点是面积和电容的增加，随之增加了延时和功耗
- 编码数据消除最坏情形的翻转能使总线加速
- 驱动大电容负载：确定合适的尺寸，把驱动器划分成逐渐增大的缓冲器链有助于解决大 Fan Out 问题$$t_p=\frac{C_LV_{swing}}{I_{av}}$$
- 给定 $t_{pmax}$ 优化 $N$ 和 $f$ （要把一个电路设计成合适的速度而不是最高的速度）
$$
A_{driver}=\frac{f^N-1}{f-1}A_{min}
$$ 

$$
E_{driver}=\frac{F-1}{f-1}(1+\gamma)C_iV_{DD}^2\approx \frac{2C_L}{f-1}V_{DD}^2
$$
- 较长的多晶线通常有很高的电阻——宽晶体管的实现：降低扩散电容、门电阻
- ESD：充电到很高的静电势若接入引线会对输入晶体管造成致命损伤
- 三态门（第二个用于驱动大电容）

### Reducing the swing
- Reducing the swing potentially yields linear reduction in delay
- Also results in reduction in power dissipation（降低动态功耗）
- 减小了噪声容限，降低信号的完整性和可靠性
- Delay penalty is paid by the receiver
- Requires use of “sense amplifier” to restore signal level （恢复较高性能）
- Frequently designed differentially (e.g. LVDS)


#### 静态降摆幅电路
- 以上电路：保证了输出恢复到 $V_{DD}$，稳定状态下无静态功耗，正反馈有助于加速翻转，但是对于较低的摆幅值时速度太慢难以接受


#### 动态降摆幅电路
利用预充电，所有输入门公用所以充电时间很快；求值器件由一下拉晶体管有条件地放电，这一过程很缓慢因为大电容 $C_{bus}$ 要通过小的下拉器件放电。
- 可以通过增加 $M_4$ 的面积来提高上拉能力
- 非对称的阈值 $V_M$ 导致非对称的噪声容限

### Resistance
- 欧姆电压降会导致系统性能的影响，因为电源电压很小的下降都会导致延时的明细增加，会引入噪声
- 电迁移：在一条导线上较长时间流过的直流电流会引起金属离子移动，导致导线断裂或另一条短路（取决于温度、晶体结构、平均电流密度）
- 电迁移与平均电流成正比，IR 电压降则与峰值电流有关

#### RC 延时
$$
T_d=0.38R_wC_w+0.69(R_dC_{out}+R_dC_w+R_wC_{out})
$$
- 采用更好的互联材料
- 插入中继器 

$$
m_{opt}=L\sqrt{\frac{0.38rc}{t_{buffer}}}=L\sqrt{\frac{0.38rc}{0.69R_dC_d(\gamma+1)}}
$$

- 采用更好的互联策略（45°）
- 优化互联结构
- 从两端驱动字线（双向驱动）、采用金属旁路（小电阻并联大电阻）

## Chapter 11: Arithmetic Circuits
### Adder
#### Complimentary Static CMOS Full Adder 
$$
C_o=AB+(A+B)C_i
$$
$$
S=A\oplus B\oplus C_i=ABC_i+(A+B+C_i)\overline{C_o}
$$ 

#### 镜像加法器 
用中间信号的函数来表达：
$$
G=AB\qquad D=\overline{A}\overline{B}\qquad P=A\oplus B
$$
$$
C_o(G,P)=G+PC_i=AB+(A+B)C_i
$$ 
$$
S(G,P)=P\oplus C_i=ABC_i+\overline{C_o}(A+B+C_i)
$$  

- The NMOS and PMOS chains are completely symmetrical.  
- A maximum of two series transistors can be observed in the carry-generation circuitry.
- When laying out the cell, the most critical issue is the minimization of the capacitance at node $C_o$. The reduction of the diffusion capacitances is particularly important.
- The capacitance at node $C_o$ is composed of 4 diffusion capacitances, 2 internal gate capacitances, and 6 gate capacitances in the connecting adder cell .
- The transistors connected to $C_i$ are placed closest to the output.
- Only the transistors in the carry stage have to be optimized for optimal speed. All transistors in the sum stage can be minimal size.

#### 传输门型加法器
它的和与进位输出有相似的延迟

#### Manchester 进位加法链
#### 超前进位加法器
由于电容原因，这一电路实现的面积也与 $N$ 成比例增加，所以建议 $N\le 4$
$$
C_{o,k}=G_k+P_kC_{o,k-1}=G_k+P_k(G_{k-1}+P_{k-1}C_{o,k-2})
$$
$$
t_p\propto \log_2(N)
$$

### Shifter
#### 
传播延时是常数，与移位的位数/移位器的规模无关


#### 对数移位器
采用分级移位的操作，控制字已编码，比如要移动五位则 101；速度取决于移位宽度，一个 $M$ 位的移位器需要 $\log_2M$ 级



> 筒形移位器适用于较小的移位器，对数移位器适用于较大的

## Chapter 12: Semiconductor Memories
### ROM
- 可以使本地字线和位线的长度（保持在一定的界限内），使存取速度变快
- 块地址只用来激活被寻址的块。未被寻址的块处于省电模式，它们的灵敏放大器和行与列译码器都不工作。这可以如所希望的那样节省很多功耗。
- OR/NOR ROM 阵列：速度快但是GND或VDD多；NOR也是有比逻辑，存在静态功耗
- NAND：简单，不用插入GND和VDD，面积小；但是是有比逻辑，NMOS不可以太多（否则电平输出会受到阈值影响），有静态电流，速度慢
- 改进有比逻辑（NOR、NAND）：利用预充电的 PMOS 管实现动态逻辑，但是这个 PMOS 也是时钟驱动的负载；但是NAND用的时候必须在下面加上 NMOS 管 $\bar{\phi}$，因为默认是导通的。

### NVRW 非挥发存储器
- 浮栅晶体管：在S和G-D之间加一个高电压可以产生一个高电场并引起电子雪崩注入，移去变成电压后电荷依然被捕获，编程形成了较高的阈值 $V_T$
- 可擦除可编程只读存储器 EPROM（通过紫外光擦除-缺点是系统外擦除）：
- 电擦除可编程只读存储器 $E^2PROM$：隧穿原理穿入穿出浮栅，有可逆性（只要把写的电压反过来就可以擦除）；问题：不容易控制移走的电荷量容易形成耗尽器件无法用标准的字线信号关断，可以用一个额外的晶体管串联（P437）
- Flash EEPROM 是对整个芯片或存储器的子部分成批进行的（擦除是有监控的），灵活性减弱，但是可以省去EEPROM的额外晶体管，减小了单元尺寸提高了集成度，下图是 NOR Flash

### RAM
- 静态 SRAM：电源提供内数据一直存储，6T面积大，速度快，差分输出改善噪声（后面接灵敏放大器）
- 动态 DRAM：定时刷新，1-3T面积小，速度慢，单端输出

#### SRAM
- M5 尺寸要小，电阻大——为了防止 $\bar{Q}$ 的电压过高，引起显著电流流过 $M_3\sim M_4$，使单元翻转；或者把位线预充电到 $V_{DD}/2$，也可以避免达到反相器的开关阈值
- **M5，M4 要小，M1，M6 要大**
- SRAM 的读写公式

#### 电阻负载 SRAM
- 用电阻代替 PMOS，简化了布线也缩小了尺寸
- 有比逻辑，存在静态功耗——希望 $R_L$ 尽量大来使静态功耗最小
- 字线预充电到 $V_{DD}$ 来解决 $t_p$ 的问题


#### DRAM 3T
- 反相位输出
- 存入 $V_{WWL}-V_Tn$
- 读取 3T 单元内容是非破坏性的，存放在单元的数据值不会受读操作的影响


#### DRAM 1T
- 写入：直接写入 $C_{BL}$ 到 $C_S$
- 读取：位线被预充电到 $V_{PRE}$，之后进行电荷的重新分配，使电压变化 
$$
\Delta V=V_{BL}-V_{PRE}=(V_{BIT}-V_{PRE})\frac{C_S}{C_S+C_{BL}}
$$
- 需要灵敏放大器读出
- 读取是破坏性的，需要刷新
- 1T要求有一个额外的电容被包括在设计中
- 可以把字线提高到高于 $V_{DD}$ 来避免阈值损失