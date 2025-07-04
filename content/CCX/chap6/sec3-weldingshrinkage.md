# Welding Shrinkage 算例

[Welding Shrinkage 算例](https://github.com/calculix/CalculiX-Examples/tree/master/Thermal/Thermal%20distortion) 展示了用于焊接变形的收缩模型，如下图所示

## 前处理文件

```{dropdown} pre.fbd
```cgx
# Flange thickness   <tf=10>
# flange width       <bf=100>
# length             <length=500>
# web thickness      <tw=10>
# web heigth         <hw=100>
# seam thickness     <a=7>
# seam offset        <dls=25>
# contact            <contact="pc-ss"> ("pc-ss" or "tie")
# Flange
seto flange
pnt p1 0 0 0
seta p1 p p1
swep flange new tra <bf/2.> 0 0 5
swep flange new tra 0 <-tf> 0 2
swep flange new tra 0 0 <length/2.> 25
setc flange
# web
seto web
copy p1 p2 tra 0 0 0
swep web p3 tra <tw/2.> 0 0 1
swep web new tra 0 <hw> 0 10
swep web new tra 0 0 <length/2.> 25
setc web
# seam
seto seam
copy p3 p4 tra 0 0 0
swep p4 p5 tra <sqrt(2.)*a> 0 0 2
swep p4 p6 tra 0 <sqrt(2.)*a> 0 2
line l1 D00H D00I 2
surf seamsec L00P L00Q l1
swep seam new tra 0 0 <length/2.-dls> 22
setc seam
# meshing
#~ #div all auto 10
elty all he8
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

## 后处理文件

