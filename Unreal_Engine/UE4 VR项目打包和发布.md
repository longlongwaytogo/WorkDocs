#UE4中VR项目的打包和发布

虽然编辑模式可以使用VR Preview模式预览VR项目，但打包项目，使其并不能自动启用VR模式运行，有说可以在项目设置中 Settings,勾选Start in VR ，但本人试过未成功，或许方法不对，后来找到两种可确运行的方法：
方法一：
在蓝图中执行命令：
![](res/VR_Publish.1.png)  
方法二：
程序启动参数添加 -vr ：  
![](res/vr_publish.2.png)  
