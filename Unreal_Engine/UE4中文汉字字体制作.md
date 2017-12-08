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
