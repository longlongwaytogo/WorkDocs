# pickup 类的使用

如何实现所有物体可以轻松被虚拟的人物拾取并进行交互呢。

在VR项目模版中，已经实现了一个简单的拾取功能：BP_PickupCube蓝图类，该类通过实现PickUpActor 接口类的Pick/Drop方法。但如何去拾取其他物体呢。。。  

  可以通过三种方法完成：  

1. 复制原来的BP_PickupCube蓝图类，双击模型，将蓝图的staticMeshComponents 改为需要拾取的模型即可，同时重命名新的蓝图类。
2. 通过BP_PickupCube蓝图类进行派生子蓝图类，打开子蓝图，修改StaticMeshComponents关联的模型为需要拾取的模型。
3. 将BP_PickupCube蓝图类作为模版，先在资源浏览器中选中BP_PickupCube蓝图类，然后在场景中选中需要拾取的模型，右键，选择Replace Actor With：BP_PickupCube，则当前所选模型具有了拾取接口，同时注意，该模型不一定可以正常移动，需要检查物理collison 是否设置。