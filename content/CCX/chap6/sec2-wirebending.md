# Wire Bending 算例

[Wire Bending 算例](https://github.com/calculix/CalculiX-Examples/tree/master/Drahtbiegen/Biegung) 展示了线材弯曲的算例，如下图所示

```{figure} ../../../images/CCX/chap6/wirebending.gif
---
width: 400px
name: sec2-fig:wirebending
---
Wire Bending 算例示意图，线材左端中心为原点（由于对称性，只计算一半区域即可）
```


```{figure} ../../../images/CCX/chap6/wirebending.png
---
width: 400px
name: sec2-fig:wirebending-1
---
Wire Bending 算例示意图，线材左端中心为原点
```


## 前处理文件

```{dropdown} pre.fbd
```cgx
# 基本变量定义
valu R 1              // 线材半径为 1
valu L 16             // 线材长度为 16
valu R1 5             // 固定圆柱半径为 5
valu R2 2             // 活动圆柱半径为 2
valu X 5              // 线材与圆柱切点的 x 坐标
valu Phi1 120     
valu DivR 2           // 线材弧向网格数量为 2
valu DivL 40          // 线材长度方向网格数量为 2
valu Div1 40          // 固定圆柱径向网格数量为 40
valu Div2 20          // 活动圆柱径向网格数量为 20

# 衍生变量定义
valu minusR * R -1    // 定义变量 minusR = R * -1
valu Zc1 + R1 R       // 定义变量 Zc1    = R1 + R
valu Zc1 * Zc1 -1     // 定义变量 Zc1    = Zc1 * -1
valu Zc2 + R2 R       // 定义变量 Zc2    = R2 + R
valu Ftol 1.1         // 定义变量 Ftol   = 1.1

# 实体构造——draht(线材)
seto draht                  // draht 开始设置
pnt p1 0 0 0                // 定义点 p1 (0,0,0)
pnt p1y 0 R 0               // 定义点 p1y (0,R,0)
pnt p1z 0 0 R               // 定义点 p1z (0,0,R)
pnt p1zn 0 0 minusR         // 定义点 plzn (0,0,-R)
line l1 p1 p1y DivR         // 定义线段集 l1：连接 p1--p1y，分成 DivR 段
line l2 p1y p1z p1 DivR     // 定义线段集 l2：以 p1 为圆心，连接 p1y 和 p1z 的圆弧，分成 DivR 段    
line l3 p1z p1 DivR         // 定义线段集 l3：连接 p1z--p1，分成 DivR 段
line l4 p1y p1zn p1 DivR    // 定义线段集 l4：以 p1 为圆心，连接 p1y 和 p1zn 的圆弧，分成 DivR     
line l5 p1 p1zn DivR        // 定义线段集 l5：连接 p1--p1zn，分成 DivR 段
surf s1 l1 l2 l3            // 定义面 s1：l1 l2 l3 围成的区域
surf s2 l1 l4 l5            // 定义面 s2：l1 l4 l5 围成的区域
swep all new tra L 0 0 DivL // 将已有实体平移 (L,0,0)，路径分为 DivL 段
setc draht                  // draht 结束设置

# 实体构造——rfix(固定辊)
pnt p2y X 1 Zc1                     // 定义点 p2y (X,1,Zc1)
seto rfix                           // 开始设置 rfix
pnt p2 X 0 Zc1                      // 定义点 p2 (X,0,Zc1)
swep rfix new tra 0 R 0 1           // 将 p2 平移 (0,R,0)，路径分成 1 段
swep rfix new tra R1 0 0 1          // 将 rfix 已有实体平移 (R1,0,0)，路径分为 1 段
swep rfix new rot p2y p2 Phi1 Div1  // 将 rfix 已有实体绕轴 p2y--p2 旋转 Phi1 度，同时将路径划分为 Div1 份
setc rfix                           // 结束设置 rfix

# 实体构造——rmov(可动辊)
pnt p3y X 1 Zc2                     // 定义点 p3y (X,1,Zc2)
seto rmov                           // 开始设置 rmov
pnt p3 X 0 Zc2                      // 定义点 p3 (X,0,Zc2)
swep rmov new tra 0 R 0 1           // 将 p3 平移 (0,R,0)，路径分成 1 段
swep rmov new tra 0 0 R2 1          // 将 rfix 已有实体平移 (0,0,R2)，路径分为 1 段
swep rmov sec1 rot p3 p3y 120 Div2  // 将 rfix 已有实体绕轴 p3y--p3 旋转 120 度，同时将路径划分为 Div2 份，记为 sec1
swep sec1 sec2 rot p3 p3y 120 Div2  // 将 sec1 绕轴 p3y--p3 旋转 120 度，同时将路径划分为 Div2 份，记为 sec2
swep sec2 sec3 rot p3 p3y 120 Div2  // 将 sec2 绕轴 p3y--p3 旋转 120 度，同时将路径划分为 Div2 份，记为 sec3
setc rmov                           // 结束设置 rmov
merg p                              // 合并所有重合点
merg l                              // 合并所有重合线
merg s                              // 合并所有重合面
merg b                              // 合并所有重合体

# 网格构造
valu Nref 1             // 定义参考节点编号 1
valu Nrot 2             // 定义旋转节点编号 2
node Nref X 0 Zc1       // 定义节点坐标，编号 Nref，坐标(X, 0, 0)
seta ref n Nref         // 定义 Nref 集中的节点集为 ref 
node Nrot X 1 Zc1       // 定义节点坐标，编号 Nrot，坐标 (X,1,Zc1)
seta rot n Nrot         // 定义 Nrot 集中的节点集为 rot
sys echo *rigid body, nset=Nrmov, ref node = Nref , rot node = Nrot > rb1.inp // 调用系统命令写入到 rb1.inp 文件中

elty all he8i           // 单元类型：所有单元，C3D8I
mesh all                // 生成所有网格
send all abq            // 导出所有网格的 abq 格式文件 all.msh
send all abq nam        // 导出带有集合名称的 abq 格式文件 all.nam

# 对称信息抓取            
seta symy s A005 A007   // 创建面集合 sysm，将 A005 和 A007 加入其中
comp symy do            // 补全包含面 symy 的线
comp symy do            // 补全包含面 symy 的点
send symy abq spc 2     // 将集合 symy 作为对称约束(Y方向约束)导出为 abq 格式文件

view edge               // 显示边
rot y                   // 从 y 轴看向模型
rot l 80                // 绕左侧（l = left）轴旋转 80°
frame                   // 显示坐标轴
zoom 1.5                // 放大 1.5 倍
ulin Nodes for symmetry constraint  // 图片下方显示***
plot n symy 6           // 显示 symy 节点集，大小为 6
hcpy png symy           // 将当前视图截图保存为 symy.png

# 线段约束
seta nodes n all                // 定义所有节点的集合为 nodes
enq nodes x0 rect 0 _ _ 0.01    // 抓取节点集 nodes 中坐标为 (0,*,*) 的节点集 x0，误差精度为 0.1
valu Tol * R Ftol               // 定义 Tol = R * Ftol
enq x0 wfix cx 0 _ 0 Tol a      // 抓取节点集 x0 中极坐标为 (0,*,0) 的节点追加到节点集 wfix 中，误差精度为 Tol
send wfix abq spc 123           // 导出 wfix 节点集为 abaqus 格式文件，采用单点约束，且在 x,y,z 方向位移限制为 0
ulin Nodes for wire constraint  // 图片下方显示***                    
plot n wfix 6                   // 显示 symy 节点集，大小为 6
hcpy png wfix                   // 将当前视图截图保存为 wfix.png

# 固定圆柱体约束
send rfix abq spc 123           // 导出 rfix 节点集为 abaqus 格式文件，采用单点约束，且在 x,y,z 方向位移限制为 0

# 接触面设置
# 设置 find
seta find s A00B       // 创建面集合 find，将 A00B 加入其中        
comp find do           // 补全包含面 find 的线
comp find do           // 补全包含面 find 的点
send find abq sur      // 导出 find 集合的 abq 格式文件 find.sur
# 设置 fdep
seta fdep s A006       // 创建面集合 fdep，将 A006 加入其中
comp fdep do           // 补全包含面 fdep 的线
comp fdep do           // 补全包含面 fdep 的点
send fdep abq sur      // 导出 fdep 集合的 abq 格式文件 fdep.sur
# 设置 mind
seta mind s A00H A00R A00M  // 创建面集合 mind，将 A00H A00R A00M 加入其中
comp mind do           // 补全包含面 mind 的线
comp mind do           // 补全包含面 mind 的点
send mind abq sur      // 导出 mind 集合的 abq 格式文件 mind.sur
# 设置 mdep
seta mdep s A004       // 创建面集合 mdep，将 A004 加入其中
comp mdep do           // 补全包含面 mdep 的线
comp mdep do           // 补全包含面 mdep 的点
send mdep abq sur      // 导出 mdep 集合的 abq 格式文件 mdep.sur

# 作接触图
rot l 150                 // 绕左侧（l = left）轴旋转 150°
rep all                   // 重绘所有实体
ulin Surfaces for contact // 图片下方显示***
plot f find t             // 画 find 中的面，颜色为 t
plus f fdep b             // 画 fdep 中的面，颜色为 b
plus f mind m             // 画 mind 中的面，颜色为 m
plus f mdep r             // 画 mdep 中的面，颜色为 r
hcpy png contact          // 将当前视图截图保存为 contact.png

# 作部件图
view elem                 // 显示单元
ulin Independent parts    // 图片下方显示***
seta ! all                // 对 all 集合中的元素进行分析，自动识别不相连的网格并分别存入新集合
hcpy png parts            // 将当前视图截图保存为 parts.png
```

## 求解器文件

```
** 包含文件
*include, input=all.msh    
*include, input=draht.nam
*include, input=rfix.nam
*include, input=rmov.nam
*include, input=ref.nam
*include, input=rot.nam
*include, input=fdep.sur
*include, input=find.sur
*include, input=mdep.sur
*include, input=mind.sur
*include, input=rb1.inp (content: *rigid body, nset=Nrmov, ref node = 1 , rot node = 2)

** 边界设置
*boundary
Nref, 1,3                     // 约束节点集 Nref 的 1-3 自由度初始为 0
Nrot, 1,3                     // 约束节点集 Nrot 的 1-3 自由度初始为 0
** 包含边界条件文件
*include, input=symy_2.bou     
*include, input=rfix_123.bou
*include, input=wfix_123.bou

** 材料设置
*material, name=draht        // 定义材料属性 draht 
*elastic                     // 弹性属性
210000,0.3                   // 弹性模量为 210000，泊松比为 0.3 
*plastic                     // 塑性属性（自定义曲线）
200,0                        // 屈服应力，此时塑性应变为 0
5000,1                       // 应力为 5000 时，此时塑性应变为 1
*material, name=tool         // 定义材料属性 tool
*elastic                     // 弹性属性
210000,0.3                   // 弹性模量为 210000，泊松比为 0.3 

** 材料属性分配
*solid section, elset=Edraht, material=draht // 分配属性 draht 给 Edraht
*solid section, elset=Erfix, material=tool   // 分配属性 tool 给 Erfix
*solid section, elset=Ermov, material=tool   // 分配属性 tool 给 Ermov

** 接触定义
*surface interaction, name=itool   // 定义表面相互作用 itool
**surface behavior, pressure-overclosure=linear
**1e6
**surface behavior, pressure-overclosure=exponential
**0.02,100
*surface behavior, pressure-overclosure=linear // 压力-重叠关系设为线性
10000,0.1,0.01                                 // 压力-闭合曲线斜率，很大间隙时的拉力，最大允许间隙
***friction
**0.1,1e7
*contact pair, interaction=itool, type=node to surface // 采用 itool 相互作用定义两个表面之间的点-面接触
Smdep,Smind                  // Smdep 与 Smind 接触
Sfdep,Sfind                  // Sfdep 与 Sfind 接触

** 分析步设置
*step,nlgeom, inc=200        // 定义一个分析步，启用几何非线性，最大增量步数量为 200
*controls, parameters=field  // 非线性求解器控制参数，收敛准则设置(field)
0.005,1,0.1,0.1              // 最大残差/平均力，最大增量解，新步初始平均力，用户自定义平均力
*static                      // 使用静力学分析
0.01,1,0.00000000000001,0.1  // 初始时间步长 0.01，总步长 1，最小步长 0.00000000000001，最大步长 0.1
*boundary                    // 边界设置
Nrot,2,2,1.57                // 对 Nrot 点集的第 2 个自由度施加 1.57 的变化（绕 y 轴旋转 90°）

** 结果输出
*node file, frequency=10     // 每 10 步输出节点量
U                            // 输出位移
*el file                     // 输出单元变量
S,PE                         // 应力，塑性应变
*contact file                // 输出接触
CDIS                         // 接触位移
*node print, nset=Nrot, frequency=1  // 每 1 步输出 Nrot 节点量
RF                                   // 输出反力
*el print, totals=only, elset=Edraht // 只输出 Edraht 单元集合的量
ELSE                                 // 单元能量
*end step                            // 结束分析步
```


## 后处理文件

```
# 读取文件
# read Biegung.inp nom // 读取文件 Biegung.frd (no mesh)
read Biegung.frd       // 读取文件 Biegung.inp

view disp              // 显示变形结构
view elem              // 显示单元
frame                  // 自动调整视图，默认使得整个模型或指定集合完全显示在当前窗口内

tra u 2                // 将模型向上平移尺寸的 2 倍
rot y                  // 从 y 轴正向看模型
rot r 130              // 绕右端旋转 130°
zoom 1.5               // 放大 1.5 倍
ds -1 e 1              // 展示倒数第二个数据集的第一个变量值
seta ! all             // 对 all 集合中的元素进行分析，自动识别不相连的网格并分别存入新集合
hcpy png deform        // 将当前截图保存为 deform.png

rot y                  // 从 y 轴正向看模型
frame                  // 自动调整视图，默认使得整个模型或指定集合完全显示在当前窗口内
text Plastic equivalent strain  // 图片下方显示*** 
ds -3 e 1              // 展示倒数第四个数据集的第一个变量值
comp Ndraht do         // 补全包含 Ndraht 点集的面
zoom 1.5               // 放大 1.5 倍
tra r 2                // 将模型向上平移尺寸的 2 倍
plot fv Ndraht         // 绘制 Ndraht 的面值(face value)视图
min 0 f                // 设置区间最小值为 0，浮点数格式
hcpy png PE            // 将当前截图保存为 PE.png



# movie
zoom 0.55             // 缩放 0.55
rot -y                // 从 y 轴负向看模型
view surf             // 显示曲面
movi delay 0.3        // 帧延迟 0.3 s
anim real             // 显示真实变形
movi frames auto      // 自动抓取
ds 2 ah 7             // 展示第 3 个数据集的第 7 个变量值的历史数据
```

## 计算结果