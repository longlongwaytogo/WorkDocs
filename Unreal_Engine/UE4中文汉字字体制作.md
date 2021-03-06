#UE4中文汉字制作  
1. 资源浏览器中右键，选择User Interface->font创建字体蓝图：MyFont。
![](res/chinese_font_1.png)  
2. 双击MyFont,打开字体编辑器，进行修改。在Detail面板，找到Font Cache Type,切换为Offline模式。弹出的对话框直接点yes就行，稍后出现字库选择面板，此处选择字体：仿宋，字号：48号,点击确认。  
 ![](res/chinese_font_2.png) 
3. 在Detail面板中chars输入需要使用的中文汉字，并勾选Alpha Only选项。  
![](res/chinese_font_3.png)    
4. 执行菜单栏  Asset->Reimport MyFont 功能，此时就会生成想要的汉字字库，不过汉字顺序并不是按照输入顺序显示
![](res/chinese_font_4.png)  
5. 创建材质文件MyFontMat，双击材质，将节点的blend Mode 改为Mask模式，创建FontSampleParameter节点和VertexColor，添加如图逻辑：  
![](res/chinese_font_5.png)   
6. 在Module中找到TextRender对象，放置到场景中，修改TextRender的material、Font属性为以上创建资源，并在Text属性输入：勇敢无畏的勇士。 

 ![](res/chinese_font_6.png) 
7. 最终效果如图：      
 ![](res/chinese_font_7.png) 

8. 对于以上字体材质，也可以使用其他连接方式：

  - 在生成font时，不勾选Alpha Only选项。
  - 连接字体材质时，使用font作为basecolor,font的alpha最为opacity 作为mask。    
 
 ![](res/font_2.png)

9. Alpha only选项的作用就是表示 Font Sample Parameter 所有的输出引脚，都输出Alpha通道，原注释是这样解释：
		if true then forces PF_G8 and only maintains Alpha value and discards color
		如果真，对于PF_G8格式,只有保持Alpha值且丢弃颜色值