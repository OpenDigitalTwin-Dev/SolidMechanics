# CalculiX 简介

[CalculiX](https://www.calculix.de/)（简称 CCX）是一个用于求解场问题的开源有限元分析（FEA）软件包。它采用有限元方法，能够完成模型的建立、计算和后处理。CalculiX 包含两个主要部分：
- ccx（CalculiX CrunchiX） 作为求解器，支持线性与非线性计算，可进行静力学、动力学和热分析
- cgx（CalculiX GraphiX） 则是交互式三维前后处理工具，基于 OpenGL 技术，便于用户进行建模和结果可视化

CalculiX 的求解器支持 ABAQUS 输入格式，因此用户可以结合商业前处理器使用。此外，cgx 还能导出适用于 Nastran、Abaqus、Ansys、Code-Aster 及多个开源 CFD 软件（如 OpenFOAM、dolfyn、duns、ISAAC）的网格数据，并内置了简单的 STEP 文件读取功能，支持多种外部 CAD 接口。CalculiX 能够在 Unix（如 Linux、Irix）以及 Windows 平台上运行

该软件由德国慕尼黑 MTU Aero Engines 的工程师团队在业余时间开发，公司也支持其公开发布。CalculiX 以其强大的功能、灵活的接口和免费的特性，在学术研究与工程实践中都得到了广泛应用

## Cubit-CalculiX

[Cubit-CalculiX](https://www.maschinenbauer.at/open-source/calculix-component-for-coreform-cubit) 是一个专为 Coreform Cubit（原名 Trelis）开发的插件组件，能让用户在 Cubit 环境下轻松完成 CalculiX 的前处理。该组件让 Coreform Cubit 成为 CalculiX 的高效前处理器，极大简化了模型定义、网格划分和后处理流程。用户可以直接在 Cubit 中完成高质量网格的生成、材料和边界条件的定义，并一键调用 CalculiX 求解，最后自动将结果转换为 Paraview 可视化格式，实现高效的后处理


**本笔记用于记录 CCX 的学习过程**