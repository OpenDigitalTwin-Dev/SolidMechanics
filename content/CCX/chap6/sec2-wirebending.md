# Wire Bending 算例

[Wire Bending 算例](https://github.com/calculix/CalculiX-Examples/tree/master/Drahtbiegen/Biegung) 展示了线材弯曲的算例，如下图所示

```{figure} ../../../images/CCX/chap6/wirebending.gif
---
width: 400px
name: sec2-fig:wirebending
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
valu X 5               
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

# Feste Rolle
pnt p2y X 1 Zc1
seto rfix
pnt p2 X 0 Zc1
swep rfix new tra 0 R 0 1
swep rfix new tra R1 0 0 1
swep rfix new rot p2y p2 Phi1 Div1
setc rfix

# bewegliche Rolle
pnt p3y X 1 Zc2
seto rmov
pnt p3 X 0 Zc2
swep rmov new tra 0 R 0 1
swep rmov new tra 0 0 R2 1
swep rmov sec1 rot p3 p3y 120 Div2
swep sec1 sec2 rot p3 p3y 120 Div2
swep sec2 sec3 rot p3 p3y 120 Div2
setc rmov
merg p
merg l
merg s
merg b

# Meshing
valu Nref 1
valu Nrot 2
node Nref X 0 Zc1
seta ref n Nref
node Nrot X 1 Zc1
seta rot n Nrot
sys echo *rigid body, nset=Nrmov, ref node = Nref , rot node = Nrot > rb1.inp

elty all he8i
mesh all
send all abq
send all abq nam

# symmetry
seta symy s A005 A007
comp symy do
comp symy do
send symy abq spc 2

view edge
rot y
rot l 80
frame
zoom 1.5
ulin Nodes for symmetry constraint
plot e all n
plot n symy 6
hcpy png symy

# constrain wire end
seta nodes n all
enq nodes x0 rect 0 _ _ 0.01
valu Tol * R Ftol
enq x0 wfix cx 0 _ 0 Tol a
send wfix abq spc 123
ulin Nodes for wire constraint
plot e all n
plot n wfix 6
hcpy png wfix

# constrain fixed cylinder
send rfix abq spc 123

# contact surfaces
# find
seta find s A00B
comp find do
comp find do
send find abq sur
# fdep
seta fdep s A006
comp fdep do
comp fdep do
send fdep abq sur
# mind
seta mind s A00H A00R A00M
comp mind do
comp mind do
send mind abq sur
# mdep
seta mdep s A004
comp mdep do
comp mdep do
send mdep abq sur

# image
rot l 150
rep all
ulin Surfaces for contact
plot f find t
plus f fdep b
plus f mind m
plus f mdep r
hcpy png contact

# parts and elements
view elem
ulin Independent parts
seta ! all
hcpy png parts
```

## 求解器文件

## 后处理文件

## 计算结果