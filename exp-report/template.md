<div class="cover" style="page-break-after:always;font-family:方正公文仿宋;width:100%;height:100%;border:none;margin: 0 auto;text-align:center;">
    </br></br>
    <span style="font-family:Source Han Sans Bold;text-align:center;font-size:25pt;margin: 10pt auto;line-height:30pt;">东南大学电子科学与工程学院</span>
    </br></br></br></br></br></br></br>
    <span style="font-family:Source Han Sans Bold;text-align:center;font-size:40pt;margin: 10pt auto;line-height:30pt;">实 验 报 告</span>
    </br></br></br></br></br></br></br>
    <span style="font-family:Source Han Sans;text-align:center;font-size:25pt;margin: 10pt auto;line-height:30pt;">课程名称：</span>
    <span style="font-family:Source Han Sans ;text-align:center;font-size:25pt;margin: 10pt auto;line-height:30pt;border-bottom: 2px solid; padding=5px;width:300px;display:-moz-inline-box;display:inline-block;">  集成电路CAD  </span>
    </br></br></br></br></br></br></br></br></br></br></br></br></br></br>
    <table style="border:none;border-collapse:separate; border-spacing:0px 10px;align:center; text-align:center;width:90%; font-family:仿宋;font-size:20pt; margin: 0 -10px; cellspacing: 15pt;">
    <tbody style="font-family:Source Han Sans;font-size:15pt;%">
    	<tr style="font-weight:normal"> 
    		<td style="width:20%;text-align:right;">实验名称</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋"> 使用 S-Edit 设计简单逻辑电路</td></tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">姓　　名</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋"> 孙寒石</td>     </tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">学　　号</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋">06219109 </td>     </tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">实验地点</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋"> 东南大学无锡国际校区</td>     </tr>
    	<tr style="font-weight:normal;"> 
    		<td style="width:20%;text-align:right;">实验时间</td>
    		<td style="width:2%">：</td> 
    		<td style="width:40%;font-weight:normal;border-bottom: 1px solid;text-align:center;font-family:华文仿宋">2022-3-25 </td>     </tr>
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


# 实验二·使用 S-Edit 设计简单逻辑电路

## 实验目的

- 进一步掌握 S-Edit 的基本操作（包括从组件库引用模块、加入联机、加入输入/输出端口、输出成 SPICE 文件等）：

- 学会利用已有模块来构成一些电路；

- 充分理解电路设计模式（Schematic Mode）和符号模式 (Symbol Mode)。

  

## 预习要求

- 复习 S-Edit 基本功能的使用；
- 掌握 MOS 管构成的与非门电路及原理；
- 掌握 MOS 管构成的或非门电路及原理。

## 实验内容及步骤（实验设计指标）
- 使用 S-Edit 编辑二输入与非门及其符号，输出 SPICE 文件；
- 使用 S-Edit 编辑二输入或非门及其符号，输出 SPICE 文件；
- 检查与非门、或非门的导出的 SPICE 文件。

## 设计过程

### 与非门（NAND2）电路与符号

我们设其输入分别为 $I_1$和 $I_2$，输出为 OUT，利用 MOS 管进行电路的设计和符号的绘制，得到如下结果。其中，在电路设计中，我们遵循 PUN 和 PDN 的设计方法，PUN 为两个 PMOS 的并联，PDN 为两个 NMOS 的串联。

电路：

<img src="C:\Users\12647\Desktop\大三下\集成电路CAD\exp2\20220325221711.png" alt="20220325221711" style="zoom:50%;" />

符号：

<img src="C:\Users\12647\Desktop\大三下\集成电路CAD\exp2\20220325223738.png" alt="20220325223738" style="zoom: 50%;" />

随后，我们可以利用 T-SPICE 得到其输出的 SPICE 文件。

<img src="C:\Users\12647\Desktop\大三下\集成电路CAD\exp2\20220325223752.png" alt="20220325223752" style="zoom:50%;" />



### 或非门（NOR2）电路与符号

我们设其输入分别为 $I_1$和 $I_2$，输出为 OUT，利用 MOS 管进行电路的设计和符号的绘制，得到如下结果。其中，在电路设计中，我们遵循 PUN 和 PDN 的设计方法，PUN 为两个 PMOS 的串联，PDN 为两个 NMOS 的并联。

<img src="C:\Users\12647\Desktop\大三下\集成电路CAD\exp2\20220325224640.png" alt="20220325224640" style="zoom: 50%;" />

符号：

<img src="C:\Users\12647\Desktop\大三下\集成电路CAD\exp2\20220325224630.png" alt="20220325224630" style="zoom:50%;" />

随后，我们可以利用 T-SPICE 得到其输出的 SPICE 文件。

<img src="C:\Users\12647\Desktop\大三下\集成电路CAD\exp2\20220325224648.png" alt="20220325224648" style="zoom:50%;" />

## 实验过程中出现的问题和体会

- PMOS 和 NMOS 的型号选错了，没有在 SPICE 库中进行选择，导致后面的 SPICE 文件无法输出
- 操作欠熟练
- 鼠标绘图能力有待提高
