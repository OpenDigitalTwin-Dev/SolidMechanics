# Tubes 算例

[Tubes 算例](https://github.com/calculix/CalculiX-Examples/tree/master/Drahtbiegen/Biegung)展现了具有伸缩结构的线弹性管在纯弯曲载荷（无剪切力）下的力学响应，如下图所示

```{figure} ../../../images/CCX/chap6/tubes.gif
---
width: 600px
name: sec1-fig:tubes
---
Tubes 算例示意图，外管左端中心为原点（由于对称性，只计算一半区域即可）
```

其中，外管内表面与内管外表面有一定的接触面积，外管左端固定，内管右端绕 $y$ 轴旋转


## 前处理文件

```{dropdown} pre.fbd
```cgx
# 基本变量定义
valu R1 50                        // 外管半径 R1  = 50
valu T1 5                         // 外管厚度 T1  = 5
valu L1 500                       // 外管长度 L1  = 500
valu R2 45                        // 内管半径 R2  = 45
valu T2 5                         // 内管厚度 T2  = 5
valu L2 500                       // 内管长度 L2  = 500
valu OVL 150                      // 重叠长度 OVL = 150
valu divt 1                       // 管厚方向网格数量 divt   = 1
valu divrot 18                    // 管沿方向网格数量 divrot = 18
valu divl 50                      // 管长方向网格数量 divl   = 50

# 衍生变量定义
valu T1neg * T1 -1                // T1neg = T1 * -1
valu T2neg * T2 -1                // T2neg = T2 * -1
valu x21 - L1 OVL                 // x21   = L1 - OVL
valu x22 + x21 L2                 // x22   = x21 + L2

# 实体构造——tube1
seto tube1                        // tube1 设置开始
pnt p1 0 0 R1                     // 定义点 p1：(0,0,R1)
swep tube1 new tra 0 0 T1neg divt // 将点 p1 平移(0,0,T1neg)，同时将路径划分为 divt 份
swep tube1 new tra L1 0 0 divl    // 将上一步结果平移(L1,0,0)，同时将路径划分为 divl 份
swep tube1 new rot x 180 divrot   // 将上一步结果绕 x 轴顺时针旋转 180°，同时将路径划分为 divrot 份
setc                              // tube1 设置结束

# 实体构造——tube2                   // 同理
seto tube2
pnt p2 x21 0 R2
swep tube2 new tra 0 0 T2neg divt
swep tube2 new tra L2 0 0 divl
swep tube2 new rot x 180 divrot
setc

# 网格构造
node 1 x22 0 0                    // 定义节点，编号 1，坐标(x22, 0, 0)
elty all he8i                     // 单元类型：所有单元，C3D8I
mesh all                          // 生成所有网格
send all abq                      // 导出所有网格的 abq 格式文件 all.msh

# 节点集定义
seta nodes n all                  // 定义全体实体的节点集为 nodes     
seta n1 n tube1                   // 定义 tube1 的节点集为 n1 
seta n2 n tube2                   // 定义 tube2 的节点集为 n2 

# 固定边界节点集抓取
enq n1 fix rec 0 _ _ 0.1          // 笛卡尔坐标筛选，抓取节点集 n1 中坐标为 (0,*,*) 的节点集 fix，误差精度为 0.1
send fix abq nam                  // 导出 fix 节点集的 abq 格式文件 fix.nam

# 对称面节点集抓取
enq nodes ysym rec _ 0 _ 0.1      // 笛卡尔坐标筛选，抓取节点集 nodes 中坐标为 (*,0,*) 的节点集 ysym，误差精度为 0.1
send ysym abq nam                 // 导出 ysym 节点集的 abq 格式文件 ysym.nam

# 边界加载作用面抓取
enq n2 load rec x22 _ _ 0.1       // 笛卡尔坐标筛选，抓取节点集 n2 中坐标为 (x22,*,*) 的节点集 load，误差精度为 0.1
send abq load                     // 导出 load 节点集的 abq 格式
comp load do                      // 补全包含 load 节点集的面(特例使用)
send load abq surf                // 导出 load 集中面的 abq 格式文件 load.sur

# 抓取外管内表面
valu R1i - R1 T1                  // 定义外管内径 R1i = R1 - T1 
enq n1 ind cx R1i _ _ 0.1         // 极坐标筛选，抓取节点集 n1 中极坐标为 (R1i,*,*) 的节点集 ind，误差精度为 0.1
comp ind do                       // 补全包含 ind 节点集的面(特例使用)
send ind abq surf                 // 导出 ind 集中面的 abq 格式文件 ind.sur  

# 抓取内管外表面
enq n2 dep cx R2 _ _ 0.1          // 极坐标筛选，抓取节点集 n2 中极坐标为 (R2,*,*) 的节点集 dep，误差精度为 0.1
comp dep do                       // 补全包含 dep 节点集的面(特例使用)
send dep abq surf                 // 导出 dep 集中面的 abq 格式文件 dep.sur  

# 计算前可视化
rot -y                            // 从 y 轴负方向看模型
plot f all n                      // 显示所有单元和节点
frame                             // 显示坐标轴
rot l 80                          // 绕左侧（l = left）轴旋转 80°
rot u 10                          // 绕上方（u = up）轴旋转 10°
plus f ind b                      // 高亮显示 ind 集为蓝色
plus f dep r                      // 高亮显示 dep 集为红色
view elem                         // 切换到单元视图
zoom 4                            // 放大视图 4 倍
hcpy png contact                  // 将当前视图截图保存为 contact.png

plot n fix m 6                    // 显示 fix 节点集的所有节点，颜色 m，尺寸 6
plus n load t 6                   // 显示 load 节点集的所有节点，颜色 t，尺寸 6
plus n ysym r 4                   // 显示 ysym 节点集的所有节点，颜色 r，尺寸 4
ulin fix (magenta), ysym (red), load (turq) // 图片下方显示***
hcpy png sets                     // 将当前视图截图保存为 sets.png
```

## 求解器文件

```{dropdown} solve.inp
```ccx
** 包含文件设置
*include, input=all.msh       // 读入全体网格
*include, input=ind.sur       // 读入外管内表面
*include, input=dep.sur       // 读入内管外表面
*include, input=load.sur      // 读入加载作用面
*include, input=fix.nam       // 读入固定面节点集
*include, input=ysym.nam      // 读入对称面节点集
*nset, nset=control           // 定义节点集 control
1                             // 包含节点 1

** 约束设置
*boundary                     // 边界约束
Nfix,1,3                      // 固定节点集 Nfix 的第 1~3 个自由度
Nysym,2                       // 固定节点集 Nysym 的第 2 个自由度

** 材料属性设置
*MATERIAL, NAME=Aluminium     // 定义材料 Aluminium 
*ELASTIC                      // 定义弹性属性
70000, 0.34                   // 弹性模量为 70000，泊松比为 0.34 
*DENSITY                      // 定义密度
2.7e-9                        // 密度为 2.7e-9
*solid section, elset=Eall, material=Aluminium  // 将材料 Aluminium 赋予到全体单元上

** 接触设置
*surface interaction, name=telescope            // 定义表面相互作用 telescope
*surface behavior, pressure-overclosure=linear  // 压力-重叠关系设为线性
100000.                                         // 刚度为 100000
*contact pair, interaction=telescope, type=surface to surface  // 采用telescope相互作用定义两个表面之间的面-面接触
Sdep,Sind                                       // 作用表面为 Sdep 和 Sind 

** 耦合设置
*coupling, ref node=1, surface=Sload, constraint name=c1  // 将节点 1（设为参考点）与 Sload 表面耦合，约束命名为 c1
*kinematic           // 采用运动学耦合
1                    // 约束自由度起始编号 1 (X)
3                    // 约束自由度终止编号 3 (Y)
*boundary            // 边界设置
control,1,2          // 固定节点集 control 的第 1~2 自由度

** 分析步与载荷设置
*step, nlgeom        // 定义一个分析步，启用几何非线性
*static              // 使用静力学分析
0.1,1,1e-5,0.05      // 初始时间步长 0.1，总步长 1，最小步长 1e-5，最大步长 0.05
*boundary            // 载荷设置
control,5,5,0.3      // 对 control 节点集的第 5 自由度(绕 y 轴旋转)施加 0.3 的变化

** 输出设置
*NODE FILE           // 节点相关信息
U                    // 节点位移
*el file             // 单元相关信息
S                    // 单元应力
*section print, surface=Sload, name=sp1 // Sload 面相关信息
SOM                  // section output moments, 截面力矩
*contact file        // 接触相关信息
CSTR                 // contact stress, 接触应力
*END STEP            // 结束分析步
```

## 后处理文件

```{dropdown} post.fbd
```cgx
wsize 1920 1080                // 窗口大小设置为 1920x1080
font l 5                       // 左侧字体大小为 5

# 读取文件
read solve.inp                 // 读取文件 solve.inp
read solve.frd                 // 读取文件 solve.frd

# 视图设置
view disp                      // 显示变形结构
view sh                        // 打开阴影显示
rot -y                         // 从 y 轴负方向看模型

# 应力排序：S11, S22, S33, S12, S13, S23, Mises 应力
# 绘制 Mises 应力云图
ds -2 e 7                      // 选择倒数第 3 个数据集的第 7 个实体
plot fv all                    // 绘制所有单元的面视图
frame                          // 显示框架
# zoom 1.5                     // 放大 1.5 倍
hcpy png SE                    // 将当前截图保存为 SE.png
zoom 4                         // 放大 4 倍
hcpy png SE_zoom               // 将当前截图保存为 SE_zoom.png

# 绘制接触应力云图
ds -1 e 4                      // 选择倒数第 2 个数据集的第 4 个实体
plot fv Sdep                   // 绘制面 Sdep 的视图
view sh off                    // 关闭阴影显示
hcpy png cpress                // 将当前截图保存为 cpress.png    
rot u 60                       // 向上旋转 60°
hcpy png cpress_rot            // 将当前截图保存为 cpress_rot.png

#sys dat2txt.py                // 运行 dat2txt.py 脚本，将dat文件转换为文本格式
#sys gnuplot moment.plt        // 运行 gnuplot 脚本 moment.plt，用于绘制力矩曲线

# movie                        // 制作 gif 动画
zoom 0.3                       // 视图缩小 0.3 倍
rot -y                         // 从 y 轴负方向看模型
rot u 45                       // 绕上侧（u = up）轴旋转 45°
rot l -30                      // 绕左侧（l = left）轴旋转 -30°
view surf                      // 显示所有面
movi delay 0.3                 // 帧延迟 0.3 s
movi frames auto               // 自动抓取帧
ds 3 ah 7                      // 选择第 3 个数据集的第 7 个实体的历史数据
```

## 计算结果

### 静力学分析求解结果

```
*static
0.1,1
```

::::{grid} 2
:margin: 0

:::{grid-item}
```{figure} ../../../images/CCX/chap6/tubes-mises-static.png
:width: 100%
:name: tubes-mises-static

静力学分析结果-Mises 应力
```
:::

:::{grid-item}
```{figure} ../../../images/CCX/chap6/tubes-cpress-static.png
:width: 100%
:name: tubes-cpress-static

静力学分析结果-接触应力
```
:::
::::
