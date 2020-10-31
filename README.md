# Unity-Anti-Aliasing
Unity关于抗锯齿的方法总结

# Unity 抗锯齿常用解决办法 https://www.cnblogs.com/mrmocha/p/9503947.html
1、用显卡的硬件抗锯齿功能
	Unity -> edit->project settings->quality  anti aliasing 选择X4或者X8
	
2、用Unity5.3.5及以上系统自带的算法组件（需要添加抗锯齿的相机勾选上）
	Unity->Camera->Allow MSAA

3、用Legacy Cinematic Image Effects插件（免费，Unity版本要求5.3.5及以上）
	导入后，选择需要添加抗锯齿的camera，add component -> anti aliasing
	
# unity中抗锯齿解决方法 https://blog.csdn.net/unityzhongdeyu/article/details/80449259
1、先去找美工查找模型的问题，看看是不是面和面之间太近，模型有重叠面，磨损的面。

2、改变一下shader，改变一下渲染方式。

3、在编辑（edit）菜单-找project setting---quality在弹出的面板里找 anti-aliasing   选择 4x或更高。

4、使用滤镜Image effect下的抗锯齿。

# unity中抗锯齿有没有什么好的解决方案? 【知乎】 https://www.zhihu.com/question/301465525
VR项目,严重模型闪烁,设置了*8的抗锯齿之后,画面闪烁的问题相对改善了许多,但是闪烁的程度还是不能被接受的.也尝试了一些抗锯齿插件,比如CTAA一类,但是随之而来的问题是由于抗锯齿带来的画面模糊,场景又较大,整个画面犹如蒙上了一层阴影.官方后处理的Post-ProcessingProfile插件里提供了TAA,不知道是否能起作用,还请问有项目经验丰富的U3D开发对这一块有没有什么好的建议
1、正向解决：	
	减少细边
	3d物体模型贴图开启mipmap
	用MSAA
	性能剩余的话提高渲染分辨率
	多关注VR相关的技术升级，利用底层硬件上的优化

2、绕路解决：
	手动模糊边缘，加一个边缘透明渐变mask
	
3、http://p.whxysz.net/kod/files/Unity-Anti-Aliasing.png

# Unity3D学习（七）：Unity多重采样抗锯齿设置无效的解决办法
学习Shader的过程中发现模型锯齿严重，于是去Edit——Project Settings——Quality选项下将反锯齿设置为了8X Multi Sampling。结果没有任何改变

1、解决办法：
	将摄像机的渲染路径（Rendering Path）设置为前向渲染（ForwardBase）就行，因为Unity默认的延迟渲染（Deffered Rendering）不支持多重采样抗锯齿（MSAA）

2、为什么多重采样抗锯齿不能在延迟渲染模式下工作？
	延迟渲染依赖于每个片段存储的数据，这是通过纹理来完成的。
	这与多重采样抗锯齿不兼容，因为抗锯齿技术依赖于子像素数据。
	虽然三角形的边缘仍然可以从多重采样抗锯齿中受益，但延迟渲染的数据仍然是混叠的。
	你将不得不依靠一个后处理过滤器来进行抗锯齿。
	
	有关延迟渲染可以参考
	Unity Rendering (13) :Deffered Shading
	中文版地址：
	Unity 渲染教程（十三）：延迟渲染
	额外参考：
	前向渲染和延迟渲染的区别
	


