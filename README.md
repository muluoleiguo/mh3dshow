一听到梦幻西游端游，可能会觉得是技术栈过早的项目，但是也不尽然，请看下文

我负责的模块是梦幻西游中近两年才开始接入的3D技术，整体的技术栈采用

美术，TA，策划，程序**编辑器**用**Unreal**4.26，程序**Runtime**采用自研引擎**Messiah**，项目流水目标是渲染还原二次元偏厚涂的风格立绘画风。此处编辑器包括了美术资产管理，TA制作的Material连连看，Gameplay相关的角色蓝图拼装，策划属性配置，程序扩展编辑器工具开发等步骤全部在Unreal中完成，采用自研的Unreal资产转换Messiah的Aurora插件，转换模型，材质，骨骼，动画，场景，特效等资产到Messiah，同时Gameplay相关的配置自动导表给Messiah。

上图是立绘效果，下图是引擎runtime渲染效果

<p style="text-align: center;">
      <img src="项目简介.assets/POPO-20240908-114057.png" alt="Image 1" style="display: inline-block; max-width: 30%;">
      <img src="项目简介.assets/POPO-20240908-115847.png" alt="Image 1" style="display: inline-block; max-width: 36%;">

分为多个模块介绍整个项目：

1、Unreal-Messiah对齐Aurora

2、

[角色渲染综述]: 角色渲染.md	"角色渲染综述"

3、Unreal编辑器工具开发

4、Messiah Runtime Gameplay介绍以及编辑器工具介绍



处于保密原因，简介中不会出现Messiah编辑器以及其相关的工具的图像，最多只有UE编辑器的展示

