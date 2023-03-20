<div class="cover" style="page-break-after:always;font-family:方正公文仿宋;width:100%;height:100%;border:none;margin: 0 auto;text-align:center;">
    </br></br>
    <span style="font-family:Source Han Sans Bold;text-align:center;font-size:25pt;margin: 10pt auto;line-height:30pt;">东南大学电子科学与工程学院</span>
    </br></br></br></br></br></br></br>
    <span style="font-family:Source Han Sans Bold;text-align:center;font-size:40pt;margin: 10pt auto;line-height:30pt;">学 习 报 告</span>
    </br></br></br></br></br></br></br>
    <span style="font-family:Source Han Sans;text-align:center;font-size:25pt;margin: 10pt auto;line-height:30pt;">课程名称：</span>
    <span style="font-family:Source Han Sans ;text-align:center;font-size:18pt;margin: 10pt auto;line-height:30pt;border-bottom: 2px solid; padding=5px;width:300px;display:-moz-inline-box;display:inline-block;">  数字模拟集成电路课程设计  </span>
    </br></br></br></br></br></br></br>
    <table style="border:none;border-collapse:separate; border-spacing:0px 10px;align:center; text-align:center;width:90%; font-family:仿宋;font-size:20pt; margin: 0 -10px; cellspacing: 15pt;">
    <tbody style="font-family:Source Han Sans;font-size:15pt;%">
    	<tr style="font-weight:normal"> 
    		<td style="width:20%;text-align:right;">学习名称</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋">有限状态机概述（Mealy&Moore）</td></tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">姓　　名</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋"> 孙寒石</td>     </tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">学　　号</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋">06219109 </td>     </tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">学习地点</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋"> 东南大学无锡国际校区</td>     </tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">学习时间</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋">2022-12-01 </td>     </tr>
        <tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">评定成绩</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋">  </td>     </tr>
        <tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">审阅教师</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋">  </td>     </tr>
    </tbody>              
    </table>
</div>

<!-- 注释语句：导出PDF时会在这里分页 -->


# 有限状态机概述（Mealy\&Moore）

## 有限状态机

（英语：finite-state machine，缩写：FSM）又称有限状态自动机（英语：finite-state automaton，缩写：FSA），简称状态机，是表示有限个状态以及在这些状态之间的转移和动作等行为的数学计算模型。

状态存储关于过去的信息，就是说：它反映从系统开始到现在时刻的输入变化。转移指示状态变更，并且用必须满足确使转移发生的条件来描述它。动作是在给定时刻要进行的活动的描述。有多种类型的动作：

- 进入动作（entry action）：在进入状态时进行
- 退出动作（exit action）：在退出状态时进行
- 输入动作：依赖于当前状态和输入条件进行
- 转移动作：在进行特定转移时进行



<img src="/Users/preminstrel/Downloads/Finite_state_machine_example_with_comments.svg.png" alt="Finite_state_machine_example_with_comments.svg" style="zoom:40%;" />

FSM（有限状态机）可以使用上面图那样的状态图（或状态转移图）来表示。此外可以使用多种类型的状态转移表。下面展示最常见的表示：当前状态（B）和条件（Y）的组合指示出下一个状态（C）。完整的动作信息可以只使用脚注来增加。包括完整动作信息的FSM定义可以使用状态表。

## Mealy Machine
Mealy machine的名字来自这个概念的提出者，在1951年写了A Method for Synthesizing Sequential Circuits的状态机的先驱G. H. Mealy。在计算理论中，米利型有限状态机（英语：Mealy machine）是基于它的当前状态和输入生成输出的有限状态自动机（更精确的叫有限状态变换器）。这意味着它的状态图将为每个转移边包括输入和输出二者。与输出只依赖于机器当前状态的摩尔有限状态机不同，它的输出与当前状态和输入都有关。但是对于每个Mealy机都有一个等价的Moore机，该等价的Moore机的状态数量上限是所对应Mealy机状态数量和输出数量的乘积加1。

$$
(|S'|=|S|*|Λ|+1)
$$

### 运作机制
Mealy机提供了密码机的一个根本的数学模型。例如考虑拉丁字母表的输入和输出，一个Mealy机可以被设计用来把给定字母的字符串（一序列输入）处理成密码字符串（一序列输出）。但是，尽管你可能使用Mealy模型来描述恩尼格玛密码机，状态图对于提供设计复杂密码机的灵活方式而言太复杂了。

Mealy状态机与Moore有限状态机不同，Mealy有限状态机的输出不单与当前状态有关，而且与输入信号的当前值有关。Mealy有限状态机的输出直接受输入信号的当前值影响，而输入信号可能在一个时钟周期内任意时刻变化，这使得Mealy有限状态机对输入的响应发生在当前时钟周期，比Moore有限状态机对输入信号的响应要早一个周期。因此，输入信号的噪声可能影响在输出的信号。

### 形式定义

Mealy机是6-元组 $(S, S_0, Σ, Λ, T, G)$，构成自：
- 状态的有限集合（$S$）
- 开始状态（也叫做初始状态）$S_0$，它是（$S$）的元素
- 输入字母表的有限集合（$Σ$）
- 输出字母表的有限集合（$Λ$）
- 转移函数（$T : S×Σ → S$）
- 输出函数（$G : S×Σ → Λ$）


## Moore Machine

摩尔型有限状态机的名字来自它的提出者，写了Gedanken-experiments on Sequential Machines的状态机先驱Edward F. Moore。在计算理论中，摩尔型有限状态机（英语：Moore machine）是指输出只由当前的状态所确定的有限状态自动机。摩尔型有限状态机的状态图对每个状态包含一个输出信号，相对于米利型有限状态机，它映射机器中的“转移”到输出。

### 运作机制
多数数字电子系统被设计为时序系统。时序系统是受限制形式的摩尔型有限状态机，它的状态只在全局时钟信号改变的时候改变。当前状态典型的存储在触发器中，而全局时钟信号连接到触发器的“时钟”输入上。时序系统是解决亚稳定性问题的一种方法。典型的摩尔型有限状态机包括组合逻辑链来把当前状态解码为输出（lambda）。当前状态一旦改变，这种改变通过这些链传播，几乎立即导致输出改变（或不改变）。有确保在这些变化在沿着链传播这段短暂时期在输出上不出现glitch的技术，但是设计出的大多数系统都忽略在短暂的转移时间的冒险。输出接着停留同样不确定（LED保持点亮，电力保持连接到电机等等），直到Moore机再次改变状态。

摩尔型有限状态机的输出只与有限状态自动机的当前状态有关，与输入信号的当前值无关。摩尔型有限状态机在时钟脉冲的有效边沿后的有限个门延后，输出达到稳定值。即使在一个时钟周期内输入信号发生变化，输出也会在一个完整的时钟周期内保持稳定值而不变。输入对输出的影响要到下一个时钟周期才能反映出来。摩尔型有限状态机最重要的特点就是将输入与输出信号隔离开来。

### 形式定义

Moore机形式定义为6-元组$\{ S, S_0, Σ, Λ, T, G \}$，构成如下：

- 状态的有限集合（$S$）
- 开始状态（也叫做初始状态）$S_0$，它是$S$的元素
- 输入字母表的有限集合（$Σ$）
- 输出字母表的有限集合（$Λ$）
- 映射状态和输入到下一个状态的转移函数（$T : S × Σ → S$）
- 输出函数（$G : S → Λ$）映射每个状态到输出字母表

在Moore机中的状态的数目大于等于在对应的Mealy机中状态的数目。