# 由于项目保密原因，不会出现内部编辑器、工具等图像，只有外放内容

[TOC]





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



如果对角色渲染比较感兴趣，可以看这一个文档，不过主要是TA的工作内容：[角色渲染.md](角色渲染.md )




## 1.Unreal对齐Messiah



Unreal和Messiah一系列对齐的技术链，首先来看下实机效果

**以下视频均为UE&Messiah双引擎同时打开 + 实机录制的同步镜头视频**

![669dcc55190e8f17e87e5f5bQvyMUhup05](README.assets/669dcc55190e8f17e87e5f5bQvyMUhup05.gif)![66863f8cf397df21f2ed3a0bRyGR200L05](README.assets/66863f8cf397df21f2ed3a0bRyGR200L05.gif)![666aea5c5a577d064f6f947aETQKRzIb05](README.assets/666aea5c5a577d064f6f947aETQKRzIb05.gif)![66588d812f7585e5abbae48dToisq0vT01](README.assets/66588d812f7585e5abbae48dToisq0vT01.gif)



## 2.Messiah自研引擎开发 TODO

由于项目的特殊性，不像UE项目直接Run In Editor就可以了，我们项目自动转换资源之后再Messiah中跑起来，如果想要调试就要用到公司自研的Sunshine编辑器的功能，实时查看游戏Runtime的对象和其属性，调整相机等。



## 3.Unreal开发

### 3.1 一个Mesh**，**可以有多层材质

其实ShellComponent就是一个**特殊的MeshComponent**，**和MeshComponent共用了Mesh**。

### 3.2 自定义ShadingModel

### 3.3 扩展编辑器

#### 3.3.1 染色编辑器

由于slate编写起来比较的痛苦，并且cpp的开发效率不是很高，梦幻西游端游UE编辑器中不少的工具都是用PyQt来实现的（网易的主流语言是python。。。），包括如下的这个染色编辑器

### 3.4 数据导出

#### 3.4.1 蓝图转换为数据

美术在Unreal中通过SkeletalMeshComponent，项目开发的ShellComponent，PrefabComponent等组合成一个Actor蓝图，要在Messiah runtime跑起来，需要对数据格式进行一次转换。

## 4.Gamplay

### 4.0 代码框架 TODO 需要重点强调展示

#### 4.0.1 协程 

这里主要是结合资源加载，烘焙染色贴图，RPC等一系列异步逻辑的同步化改造来说

#### 4.0.2 逻辑Plugin化

结合打包，Runtime，Editor来说

#### 4.0.3 SubSystem + View

#### 4.0.4 网络

项目的网络架构非常的特殊，不是经典的C/S架构，由于梦幻西游端游是一款多开的游戏，并且2D部分引擎采用的是古早[云风](https://blog.codingnow.com/)开发的风魂引擎，由于历史原因，重构为3D引擎不太可能，因此Runtime的Messiah引擎是独立的渲染进程，通过共享内存和风魂的中心进程通信，然后风魂再和服务端发起rpc通信。

这个架构可以看作C/S/S

其中Client就是Messiah的客户端，接入了业界认可度比较高的网易经典的Mos框架并且为了梦幻西游端游项目改造新增一层中间层。



### 4.1 动画系统

#### 4.1.1 ik的应用，其中还有输出OpenPose数据生成AI图像的玩法

![ik](README.assets/ik.gif)

#### 4.1.2 TODO

结合CharacterEditor的扩展一起

还可以结合脚本状态机

别忘了自定义成就秀





### 4.2 换装



由于整个3D玩法的基调就是类似叠纸的奇迹暖暖的换装游戏，因此这一块是最重要的Gameplay之一。

首先请看视频

TODO: 视频演示。



首先从整个角色的构成来说

角色由

* 身体的主要骨骼
* 脸部骨骼
* 挂接物的骨骼
* 软骨

现在的身体主要骨骼一共有4种体型（男，女，巨人，虎头怪），19角色对应的脸部。挂接物都是可以通用的。



从换装的逻辑上来说分为三个大的模块

1、装备(Equip)

2、资产模型(Prefab) 或者可以叫做SkeletalMesh以及其Skeleton甚至是StaticMesh

3、挂接处理(Attachment)



#### 4.2.1、装备(Equip)

**策划要求小件装备替换大件装备**

装备id001有一个腰带(waistpendant001)和衣服(cloth001)，那么穿上一个id002的腰带(waistpendant002)时候，就会顶掉`id001`中的腰带(waistpendant001)但是保留了`(cloth001)`，脱下`id002`的时候`waistpendant00001`又出现了，因此数据结构设计上就是**优先队列**，一个Equip(装备)中有的Prefab(资产模型)都同时存在，只不过优先级最高的显示而已。如此以来就非常容易理解了。

不过还需要理解一个东西，那就是人的身体是很神奇的，可以挂得满满当当的，所以一定不能把槽位(比如腰带在腰上，但是腰部是很大的空间，可以同时有腰带和比如腰包)固定死，这个应该是一个可以自由扩展的东西



#### 4.2.2、资产模型(Prefab) 

这一部分主要是由于项目的特殊性，即商业引擎**Unreal**编辑-》自研引擎**Messiah**运行差异导致的，如果在Unreal中加载SkeletalMesh资源不论是同步的还是异步的都是直接了当的，有SkeletalMeshComponent来打辅助很方便。但是对于Messiah而言，重要的是把美术编辑的数据转换为Messiah可以识别的格式并且Runtime用相应的逻辑使用这些数据。

这里结合项目组开发的ShellComponent来讲解

TODO:



#### 4.2.3、挂接

TODO: 这里主要是结合AnimationBlueprint来讲解， 怎么做挂接物的动画同步，在各种编辑器中如何适配的



### 4.3 妆容 TODO



### 4.4 染色

![染色3](README.assets/染色3.gif)



独特的染色Gameplay（用染色shader对贴图染色而非给shader传参数）

- 一般的染色， 都是 Tint(color， tint_color) x PBR, 染色做材质里面

- 但是这样有以下问题

  - 指令数--HSV染色就会有100个指令
  - 耦合--只要有东西忘记处理，就会出问题，并且逻辑上比较复杂，每个材质都有自己的染色逻辑，客户端代码也不容易组织。

- 梦幻西游采取二段

  染色

  - 染色shader作用在base/emissive**贴图**上， 贴图动态被染色然后回传材质。

    所有的材质染色逻辑统一，客户端代码也是高度统一的。

  - 这样**材质复杂度和染色复杂度**无关--染色shader可以做的很复杂

- 二段染色需要注意的

  - 上面已经写了，所有会影响最终表现颜色的，最好**和基础颜色贴图, 自发光贴图挂钩**

  - 如果最终有个颜色叠加上去又不挂钩， 最终就没法染出好的结果，

    譬如颜色公式是 PBR(base_map) + fresnel, 这样怎么染色fresnel都叠了奇怪的颜色上去

比较重要的是，梦幻西游的特效采用的Shell材质，只有少部分特殊实现（比如妆容的特效）是Unreal的Cascade转换为Messiah的Particle。因此特效也是在整个染色逻辑中的一部分，高度统一。

染色玩法框架和工具稳定之后，新出的材质的染色完全不需要程序介入，美术TA策划自己玩就好了。参考

[染色编辑器.md]()

玩法中还有如图的染色部位高光表现和UI对应的染色。

由于染色的组合数非常多，也就意味着如果是UI出资源的话会导致美术累死，因此如果UI需要染色对应的表现，也是用shader实现，但是由于角色的染色shader比较复杂，UI的染色逻辑经过了简化，看起来差不多就行。

![image](README.assets/image.png)

简化后的UI的染色shader大致的实现可以在shadertoy上进行预览

https://www.shadertoy.com/view/lX2XzV



### 4.5 剧情

之前有说到，项目的架构是采用Unreal作为编辑器，Messiah作为Runtime。

剧情编辑是一个逻辑业务上非常难以处理的存在。

整体的技术栈为Unreal的sequence转换为Messiah的Montage。





## 5、自动化

### 5.1 自动化构建

美术上传资源，策划修改配置，程序修改代码之后，到最后能够让QA跑起来的过程都是自动化构建部署在TeamCity上的，包括引擎Build，编译Shader，RefreshShaderGraph，资源代码Cook，合并分支等众多流程

### 5.2 自动化测试

截图对比自动化回归