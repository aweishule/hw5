#<center> 数字图像处理第五次作业</center>

------

<center>自动化少61</center>

<center>魏俊哲</center>

<center>2140506024</center>

<center>2019.4.2</center>

### 摘要：
本次作业学习了频域滤波器的使用，学习了butterworth and Gaussian低通和高通滤波器，laplacian和unmask高通滤波器。对频域高频分量和低频分量的理解进一步加深，掌握了频域图像处理的方法。

> 1.频域低通滤波器：设计低通滤波器包括 butterworth and Gaussian (选择合适的半径，计算功率谱比),平滑测试图像test1和2;分析各自优缺点；

### 原理说明
1)频率域滤波步骤：
①给定一幅大小为 $M \times N$ 的输入图像 f（x，y），确定填充参数， 典型的选取 P=2M 和 Q=2N ；
②对 f（x，y）添加必要数量的 0，形成大小为 $P \times Q$ 的填充后的图像 fp（x，y）； 
③用$-1^{x+y}$乘以 fp（x，y）移到其变换中心； 
④计算来自步骤 3 的图像的 DFT，得到 F(u,v)；
⑤生成一个实的、对称的滤波函数 H(u,v) ，其大小为 $P \times Q$ ，中心在（ ${P} \over  {2}$，${Q} \over  {2}$）处，用阵 列相乘形成乘积 $G(i,k)=H(i,k) \times F(i,k)$  ； 
⑥得到处理后的图像gp(x,y);
⑦通过从 gp(x,y)的左上象限提取$M \times N$ 区域，得到最终的处理结果个 g(x,y)。 
2)布特沃斯低通滤波器：
截止频率位于距原点 D0 处的 n 阶布特沃斯低通滤波器的传递函数定义为:
$H(u,v)= {{1} \over {1+[D(u,v)/D_0]^{2n}}}$其中,$D(u,v)=[(u-P/2)^2+(v-Q/2)^2]$
3)高斯低通滤波器：
$H(u,v)= e^{-D^2(u,v)/2D^2_0}$
其中， D(u,v) 是距离频率域矩形中心的距离。 D0 是截止频率。当 D(u,v)=D0 时，GLPF 下降到其最大值的 0.607 处。
4)对于功率谱的计算，只需将 F(u,v)和 G(u,v)遍历，并在每一个 (u,v)处计 算其功率谱分量并求和，最后，两者做商既得功率谱比。只给出一组作对比。 
5)使用到的MATLAB 函数： fft2 函数用于数字图像的二维傅立叶变换； 
ifft2 函数用于数字图像的二维傅立叶反变换； 
fftshift 函数用于将变换后的图象频谱中心从矩阵的原点移到矩阵的中心。 

### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20f25.bmp)
功率谱比0.8606
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20f75.bmp)
功率谱比0.9629
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t2%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t2%20f25.bmp)
功率谱比0.8762
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t2%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t2%20f75.bmp)
功率谱比0.9473
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20f25.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20f75.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t2%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20f25.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t2%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t2%20f75.bmp)


### 结果分析
 ①对比每组图像处理结果中的原始图像和低通滤波后的图像， 可以清晰看到低通滤波器的平滑效果（模糊效果）； 对比每组图像中原始图像的傅里叶谱、低通滤波器傅里叶谱以及滤波 后图像的傅里叶谱， 可以看到滤波在空间域是卷积关系和在频率域是相乘关系。 低通滤波器 对于低频分量可以通过， 而对于高频分量则不能通过。 通过三幅图的对比， 可以清晰的看到 滤波器的截断效果。 
 ②对于 test1分别选取 D0=25 、75 的二阶布特沃斯低通滤波器进行低通滤波。对比不同的 D0 值得到的结果知，随着截止频率 D0 的减小，滤波后的图像越来越模糊，功率谱比越来越小，即滤波后包含的低频分量越来越少。
 ③对于 test2 分别选取 D0=25、75 的二阶布特沃斯低通滤波器进行低通滤波。对比不同的 D0 值得到的结果知，随着截止频率 D0 的减小，滤波后的图像越来越模糊，功率谱比越来越小，即滤波后包含的低频分量越来越少。
 ④对于 test1 分别选取 D0=25 、75 的高斯低通滤波器进行低通滤波。对比不同的 D0 值 得到的结果知，随着截止频率 D0 的减小，滤波后的图像越来越模糊，功率谱比越来越小， 即滤波后包含的低频分量越来越少。
 ⑤对于 test2分别选取 D0=25、75 的高斯低通滤波器进行低通滤波。 对比不同的 D0 值得到的结果知，随着截止频率 D0 的减小，滤波后的图像越来越模糊，功率谱比越来越小， 即滤波后包含的低频分量越来越少。 
 ⑥最后， 对比二阶布特沃斯低通滤波器和高斯低通滤波器的效果知， 两种滤波器达到的基本效果是一致的， 即平滑图像， 滤除高频分量， 保留低频分量。 但两者在相同截止频率 D0 时， 得到的功率谱比却不同，主要原因是两个滤波器在过渡带处的差异。
> 2.频域高通滤波器：设计高通滤波器包括butterworth and Gaussian，在频域增强边缘。选择半径和计算功率谱比，测试图像test3,4：分析各自优缺点；

布特沃斯高通滤波器：
截止频率位于距原点 D0 处的 n 阶布特沃斯低通滤波器的传递函数定义为:
$H(u,v)= {{1} \over {1+[D_0/D(u,v)]^{2n}}}$其中,$D(u,v)=[(u-P/2)^2+(v-Q/2)^2]$
高斯低通滤波器：
$H(u,v)= 1-e^{-D^2(u,v)/2D^2_0}$
其中， D(u,v) 是距离频率域矩形中心的距离。 D0 是截止频率。当 D(u,v)=D0 时，GLPF 下降到其最大值的 0.607 处。
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t3%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t3%20f25.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t3%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t3%20f75.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t4%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t4%20f25.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t4%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/butter%20t4%20f75.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t3%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t3%20f25.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t3%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t3%20f75.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t4%20d025.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t4%20f25.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t4%20d075.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/guass%20t4%20f75.bmp)
### 结果分析
①对比每组图像处理结果中的原始图像和高通滤波后的图像， 可以清晰看到高通滤波器的边 缘增强效果； 对比每组图像中原始图像的傅里叶谱、 低通滤波器傅里叶谱以及滤波后图像的 傅里叶谱， 可以看到滤波在空间域是卷积关系和在频率域是相乘关系。 高通滤波器对于低频 分量的滤除和对于高频分量的保留作用。 通过三幅图的对比， 可以清晰的看到滤波器的截断 效果。 
②对于 test3分别选取 D0=25 、75 的二阶布特沃斯高通滤波器进行高通滤波。对比不同 的 D0 值得到的结果知，随着截止频率 D0 的增加，滤波后的图像边缘应该越来越清晰，功率谱比越来越小，即滤波后包含的高频分量越来越少。
③对于 test4 分别选取 D0=25、75 的二阶布特沃斯高通滤波器进行高通滤波。对比不同的
D0 值得到的结果知，随着截止频率 D0 的增加，滤波后的图像边缘应该越来越清晰，功率谱比越来越小，即滤波后包含的高频分量越来越少。
④对于 test3 分别选取 D0=25 、75 的高斯高通滤波器进行高通滤波。对比不同的 D0 值 得到的结果知，随着截止频率 D0 的增加，滤波后的图像边缘应该越来越清晰，功率谱比越来越小，即滤波后包含的高频分量越来越少。
⑤对于 test4 分别选取 D0=25 、75 的高斯低通滤波器进行低通滤波。对比不同的 D0 值得到 的结果知，随着截止频率 D0 的增加，滤波后的图像边缘应该越来越清晰，功率谱比越来越 小，即滤波后包含的高频分量越来越少。 
⑥对比二阶布特沃斯高通滤波器和高斯高通滤波器的效果知， 两种滤波器达到的基本效果是 一致的，即增强图像边缘，滤除低频分量，保留高频分量。但两者在相同截止频率 D0 时， 得到的功率谱比却不同，主要原因是两个滤波器在过渡带处的差异。 
⑦对比高通滤波器和低通滤波器知， 高通滤波器在滤波的时候会将直流分量也一同滤除， 导致图像变暗。造成当 D0 增大到一定程度时，边缘将不见，整个图像变为黑色不明显。 

> 3.其他高通滤波器：拉普拉斯和Unmask，对测试图像test3,4滤波；分析各自优缺点；
比较并讨论空域低通高通滤波（Project3）与频域低通和高通的关系；

### 1.拉普拉斯
### 原理说明
频域拉普拉斯算子如下：
$H(u,v)= -4\pi^2D^2(u,v)$

### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/lap%20t3%20d.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/lap%20t3%20f.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/lap%20t4%20d.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/lap%20t4%20f.bmp)
### 2.Unmask
### 原理说明
将高频分量与原图像相加，可以更好地突出边缘部分
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/unmask%20t3%20d.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/unmask%20t3%20f.bmp)

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/unmask%20t4%20d.bmp)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/hw5/master/unmask%20t4%20f.bmp)
### 结果分析
对比每组图像处理结果中的原始图像和滤波后的图像，可以隐约看到滤波器的边缘增强效果；由于最后得到的高频图像要加到原始图像上构成新的图像，所以肉眼看来原始图像的傅里叶谱和滤波后图像的傅里叶谱基本一致。
对比拉普拉斯算子和 unmask 滤波，两者达到的基本效果是一致的。

###比较并讨论空域低通高通滤波（ Project3）与频域低通和高通的关系。
空间域和频域滤波间的纽带是卷积定理。空间域中的滤波定义为滤波函数 h（x，y）与输入图像 f（x，y）进行卷积；频率域中的滤波定义为滤波函数 H（u，v）与输入图像的傅里叶 变换 F（u，v）进行相乘。空间域的滤波器和频率域的滤波器互为傅里叶变换。 频域增强技术与空域增强技术有密切的联系。 一方面， 许多空域增强技术可借助频域概念来 分析和帮助设计； 另一方面， 许多空域增强技术可转化到频域实现， 而许多频域增强技术可 转化到空域实现。 空域滤波主要包括平滑滤波和锐化滤波。 平滑滤波是要滤除不规则的噪声 或干扰的影响， 从频域的角度看， 不规则的噪声具有较高的频率， 所以可用具有低通能力的
频域滤波器来滤除。 由此可见空域的平滑滤波对应频域的低通滤波。 锐化滤波是要增强边缘 和轮廓处的强度， 从频域的角度看， 边缘和轮廓处都具有较高的频率， 所以可用具有高通能 力的频域滤波器来增强。 由此可见， 空域的锐化滤波对应频域的高通滤波。 频域里低通滤波 器的转移函数应该对应空域里平滑滤波器的模板函数的傅里叶变换。 频域里高通滤波器的转移函数应该对应空域里锐化滤波器的模板函数的傅里叶变换。 即空域和频域的滤波器组成傅 里叶变换对。 给定一个域内的滤波器， 通过傅里叶变换或反变换得到在另一个域内对应的滤 波器。空域的锐化滤波或频域的高通滤波可用两个空域的平滑滤波器或两个频域的低通滤波 器实现。 在频域中分析图像的频率成分与图像的视觉效果间的对应关系比较直观。 空域滤波 在具体实现上和硬件设计上有一定优点。 区别：例如，空域技术中无论使用点操作还是模板 操作， 每次都只是基于部分像素的性质， 而频域技术每次都利用图像中所有像素的数据， 具有全局性，有可能更好地体现图像的整体特性，如整体对比度和平均灰度值等。

### 附录
参考文献：Rafael C. Gonzalez., et al. 数字图像处理（第三版）, 电子工业出版社，2011.

