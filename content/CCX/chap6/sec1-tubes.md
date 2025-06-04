# Tubes 算例




## 前处理文件

```{dropdown} pre.fbd
```cgx
# 变量直接定义赋值
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

# 变量依赖定义赋值
valu T1neg * T1 -1                // T1neg = T1 * -1
valu T2neg * T2 -1                // T2neg = T2 * -1
valu x21 - L1 OVL                 // x21   = L1 - OVL
valu x22 + x21 L2                 // x22   = x21 + L2

# 实体构造——tube1
seto tube1                        // tube1 设置开始
pnt p1 0 0 R1                     // 定义圆 p1，中心为(0,0)，半径为 R1
swep tube1 new tra 0 0 T1neg divt // 将圆 p1 在厚度方向扩展 T1neg，划分为 divt 份
swep tube1 new tra L1 0 0 divl    // 将上一步结果在长度方向扩展 L1，划分为 divl 份
swep tube1 new rot x 180 divrot   // 将上一步结果取 180°（半圆），划分为 divrot 份
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
send all abq                      // 生成所有网格的 abq 格式文件 all.msh

# 节点集定义
seta nodes n all                  // 定义全体实体的节点集为 nodes     
seta n1 n tube1                   // 定义 tube1 的节点集为 n1 
seta n2 n tube2                   // 定义 tube2 的节点集为 n2 

# 固定边界节点集抓取
enq n1 fix rec 0 _ _ 0.1          // 笛卡尔坐标筛选，抓取节点集 n1 中坐标为 (0,*,*) 的节点集 fix，误差精度为 0.1
send fix abq nam                  // 生成 fix 节点集的 abq 格式文件 fix.nam

# 对称面节点集抓取
enq nodes ysym rec _ 0 _ 0.1      // 笛卡尔坐标筛选，抓取节点集 nodes 中坐标为 (*,0,*) 的节点集 ysym，误差精度为 0.1
send ysym abq nam                 // 生成 ysym 节点集的 abq 格式文件 ysym.nam

# 边界条件作用面抓取
enq n2 load rec x22 _ _ 0.1       // 笛卡尔坐标筛选，抓取节点集 n2 中坐标为 (x22,*,*) 的节点集 load，误差精度为 0.1
send abq load                     // 生成 load 节点集的 abq 格式
comp load do                      // 获取 load 节点集的所有下游单元(down)：线/面/体
send load abq surf                // 生成 load 集中面的 abq 格式文件 load.sur

# 抓取外管内表面
valu R1i - R1 T1                  // 定义外管内径 R1i = R1 - T1 
enq n1 ind cx R1i _ _ 0.1         // 极坐标筛选，抓取节点集 n1 中极坐标为 (R1i,*,*) 的节点集 ind，误差精度为 0.1
comp ind do                       // 获取 ind 节点集的所有下游单元(down)：线/面/体
send ind abq surf                 // 生成 ind 集中面的 abq 格式文件 ind.sur  

# 抓取内管外表面
enq n2 dep cx R2 _ _ 0.1          // 极坐标筛选，抓取节点集 n2 中极坐标为 (R2,*,*) 的节点集 dep，误差精度为 0.1
comp dep do                       // 获取 dep 节点集的所有下游单元(down)：线/面/体
send dep abq surf                 // 生成 dep 集中面的 abq 格式文件 dep.sur  

# 计算前可视化
rot -y                            // 绕 y 轴旋转模型
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
ulin fix (magenta), ysym (red), load (turq) // 图片下方显示图例
hcpy png sets                     // 将当前视图截图保存为 sets.png
```

## 求解器文件

## 后处理文件