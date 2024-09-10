# 处于项目保密原因，简介中不会出现内部编辑器、工具等图像，只有外放内容



一听到梦幻西游端游，可能会觉得是技术栈过早的项目，但是也不尽然，请看下文

> 1、注意动态图像gif比较大，直接web预览可能需要一些加载时间 



我负责的模块是梦幻西游中近两年才开始接入的3D技术，整体的技术栈采用

美术，TA，策划，程序**编辑器**用**Unreal**4.26，程序**Runtime**采用自研引擎**Messiah**，项目流水目标是渲染还原二次元偏厚涂的风格立绘画风。

此处Unreal编辑器的职责包括但不限于

* 美术资产管理，
* TA制作的Material连连看，
* Gameplay相关的角色蓝图拼装，
* 策划属性配置，
* 程序扩展编辑器
* 程序开发引擎功能

采用自研的Unreal资产转换Messiah的插件，转换模型，材质，骨骼，动画，场景，特效等资产到Messiah，同时Gameplay相关的配置自动导表给Messiah，Runtime对齐 Unreal。

上图是立绘效果，下图是Messiah引擎Runtime渲染效果

<p style="text-align: center;">
      <img src="项目简介.assets/POPO-20240908-114057.png" alt="Image 1" style="display: inline-block; max-width: 30%;">
      <img src="项目简介.assets/POPO-20240908-115847.png" alt="Image 1" style="display: inline-block; max-width: 36%;">

分为多个模块介绍整个项目：

1、[Unreal对齐Messiah](Unreal对齐Messiah.md)

2、[角色渲染.md](角色渲染.md )

3、Unreal开发

​	3.1、[染色编辑器](工具/染色编辑器.md)

4、Messiah Runtime Gameplay介绍以及编辑器工具介绍

​	4.1、[角色换装](Gameplay/角色换装.md)

​	4.2、[妆容系统](Gameplay/妆容系统.md)

​	4.3、[角色染色](Gameplay/角色染色.md)

​	4.3、[动画系统](Gameplay/动画系统.md)

​	4.4、[剧情演出](Gameplay/剧情演出.md)

​	4.5、[网络同步](Gameplay/网络同步.md)

​	4.6、[协程应用](Gameplay/协程应用.md)



