# Welding 算例

[Welding 算例](https://github.com/calculix/CalculiX-Examples/tree/master/Thermal/Thermal%20distortion) 展示了用于焊接变形的冷却收缩模型，如下图所示


## 关键特征

- 大变形
- 塑性本构
- 点面接触


## 前处理文件

注意，该文件需要由 `param.py` 进行**变量替换**，得到 `pre.fbd`，再由 `cgx` 处理，具体参照 `test.py`（为了便于理解，此处不做替换）

```{dropdown} par.pre.fbd
```cgx
# Flange thickness   <tf=10>
# flange width       <bf=100>
# length             <length=500>
# web thickness      <tw=10>
# web heigth         <hw=100>
# seam thickness     <a=7>
# seam offset        <dls=25>
# contact            <contact="pc-ss"> ("pc-ss" or "tie")

# Flange                                  // 水平板
seto flange                               // 开始设置水平板   
pnt p1 0 0 0                              // 定义点 p1 (0,0,0)
seta p1 p p1                              // 选出 p1 中的点定义为 p1
swep flange new tra <bf/2.> 0 0 5         // 将 flange 实体平移 (<bf/2.>,0,0)，轨迹分为 5 段
swep flange new tra 0 <-tf> 0 2           // 将 flange 实体平移 (0,<-tf>,0)，轨迹分为 2 段
swep flange new tra 0 0 <length/2.> 25    // 将 flange 实体平移 (0,0,<length/2.>)，轨迹分为 25 段
setc flange                               // 结束设置水平板

# web                                     // 设置竖直板
seto web                                  // 开始设置竖直板     
copy p1 p2 tra 0 0 0                      // 复制 p1，得到 p2，不发生平移 
swep web p3 tra <tw/2.> 0 0 1             // 将 web 实体平移 (<tw/2.>,0,0)，轨迹分为 1 段
swep web new tra 0 <hw> 0 10              // 将 web 实体平移 (0,<hw>,0)，轨迹分为 10 段
swep web new tra 0 0 <length/2.> 25       // 将 web 实体平移 (0,0,<length/2.>)，轨迹分为 25 段
setc web                                  // 结束设置竖直板

# seam                                    // 设置焊缝
seto seam                                 // 开始设置焊缝
copy p3 p4 tra 0 0 0                      // 复制 p3，得到 p4，不发生平移
swep p4 p5 tra <sqrt(2.)*a> 0 0 2         // 将 p4 平移 (\sqrt{2}a,0,0) 得到 P5，路径分为两段
swep p4 p6 tra 0 <sqrt(2.)*a> 0 2         // 将 p4 平移 (0,\sqrt{2}a,0) 得到 p6，路径分为两段
line l1 D00H D00I 2                       // 推测 D00H 和 D00I 分别是 p5 和 p6
surf seamsec L00P L00Q l1                 // 推测 L00P 和 L00Q 分别是线 p4-p5 和线 p4-p6
swep seam new tra 0 0 <length/2.-dls> 22  // 将 seam 平移 (0,0,length/2.-dls)，路径分为 22 段
setc seam                                 // 结束设置焊缝

# meshing                                 // 网格化
#~ #div all auto 10
elty all he8                              // 单元类型：所有单元，C3D8
#mesh flange
#mesh web
mesh all
send all abq
# z symmetry boundary
seta symz s A001 A007 seamsec
comp symz do
send symz abq spc 3
# x symmetry boundary
seta symx s A005 A00B
comp symx do
send symx abq spc 1
# y rigid body constraint
send p2 abq spc 2
# contact web-seam
seta wind s A00C
comp wind do
comp wind do
send wind abq sur
seta wdep s A00F
comp wdep do
comp wdep do
send wdep abq sur
# contact flange-seam
seta find s A003
comp find do
comp find do
send find abq sur
seta fdep s A00E
comp fdep do
comp fdep do
send fdep abq sur
# write the element sets
send all abq nam
sys cp <contact>.inc contact.inc
# write parameter for post-processing
sys echo valu contact <contact> > contact.fbd
view elem
rot -z
rot r 15
rot u 10
frame
zoom 2
seta ! all
#~ plot f flange r
#~ plus f web g
#~ plus f seam b
hcpy png
sys mv hcpy_1.png parts.png

# plot of the contact pairs
view ill
move seam tra 0.1 0.1 0
rot -z
rot r 30
rot u 30
frame
zoom 1.3
ulin Contact flange-seam (blue-turq.), web-seam (red-mag.)
plot f wind r 6
plus f wdep m 6
plus f find b 6
plus f fdep t 6
hcpy png
sys mv hcpy_2.png contact.png

ulin Planes of symmetry
rep all
plot si symz
plus si symx
hcpy png
sys mv hcpy_3.png symmetry.png

ulin Point for y constraint (web)
plot n p2 r 8
hcpy png
sys mv hcpy_4.png y-const.png
```

## 求解文件

```{dropdown} Tjoint.inp
```ccx
*include, input=all.msh
*include, input=flange.nam
*include, input=web.nam
*include, input=seam.nam
*include, input=contact.inc
**constraints
*boundary
*include, input=symx_1.bou
*include, input=symz_3.bou
*include, input=p2_2.bou
** material definition
*material, name=steel
*elastic
210000,0.3
*expansion
12e-6
*conductivity
50.,0
*specific heat
5e8,0
** material assignment to bodies
*solid section, elset=Eall, material=steel
** contact definitions
*initial conditions, type=temperature
Nall, 0
*step
*static
0.1, 100, 0.1, 1
*temperature
Nflange,0
Nweb,0
Nseam,-1000
*node file
U
*el file
S
*end step
```


## 后处理文件

```{dropdown} post.fbd
```cgx

read Tjoint.frd new
read contact.fbd

ds -1 e 7
view disp
view elem
scal d 20

seta base all
copy all new mir x
copy all new mir z
comp new do

frame
rot -z
zoom 4
rot r 6
rot u 6
tra u 20

# stress plot
ulin contact: contact
plot f new n
view sh off
plus fv base
max 3000 f
min 0 f
steps 20

valu name -SE.png
valu name & contact name
hcpy png
sys mv hcpy_1.png name

# displacement plot
valu name -D2.png
valu name & contact name
steps 10
ds -2 e 2
max 0.5 f
min -0.5 f
plot f all n
plus fv base
hcpy png
sys mv hcpy_2.png name
```