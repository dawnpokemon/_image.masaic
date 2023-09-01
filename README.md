# _image.masaic
图像拼接算法
## 图像拼接算法的分类

图像拼接作为这些年来图像研究方面的重点之一，国内外研究人员也提出了很多拼接算法。图像拼接的质量，主要依赖图像的配准程度，因此图像的配准是拼接算法的核心和关键。根据图像匹配方法的不同仁阔，图像拼接算法可分为基于“空间域”和“频域”。

基于空间域的图像拼接可以进一步划分为基于区域的图像拼接和基于特征的图像拼接。基于特征的图像拼接可以再细分为基于底层特征的图像拼接（low level feature-based image mosaicing）和基于轮廓的图像拼接（contour-based image mosaicing）。基于底层特征的拼接可以分为四类：基于Harris角点检测器的拼接、基于FAST角点检测器的拼接、基于SIFT特征检测器的拼接、以及基于SURF特征检测器的拼接。

### 基于区域相关的拼接算法

这是最为传统和最普遍的算法。基于区域的配准方法是从待拼接图像的灰度值出发，对待配准图像中一块区域与参考图像中的相同尺寸的区域使用最小二乘法或者其它数学方法计算其灰度值的差异，对此差异比较后来判断待拼接图像重叠区域的相似程度，由此得到待拼接图像重叠区域的范围和位置，从而实现图像拼接。也可以通过FFT 变换将图像由时域变换到频域，然后再进行配准。对位移量比较大的图像，可以先校正图像的旋转，然后建立两幅图像之间的映射关系。
当以两块区域像素点灰度值的差别作为判别标准时，最简单的一种方法是直接把各点灰度的差值累计起来。这种办法效果不是很好，常常由于亮度、对比度的变化及其它原因导致拼接失败。另一种方法是计算两块区域的对应像素点灰度值的相关系数，相关系数越大，则两块图像的匹配程度越高。该方法的拼接效果要好一些，成功率有所提高。

### 基于特征相关的拼接算法

基于特征的配准方法不是直接利用图像的像素值，而是通过像素导出图像的特征，然后以图像特征为标准，对图像重叠部分的对应特征区域进行搜索匹配，该类拼接算法有比较高的健壮性和鲁棒性。
基于特征的配准方法有两个过程：特征抽取和特征配准。首先从两幅图像中提取灰度变化明显的点、线、区域等特征形成特征集冈。然后在两幅图像对应的特征集中利用特征匹配算法尽可能地将存在对应关系的特征对选择出来。一系列的图像分割技术都被用到特征的抽取和边界检测上。如canny 算子、拉普拉斯高斯算子、区域生长。抽取出来的空间特征有闭合的边界、开边界、交叉线以及其他特征。特征匹配的算法有：交叉相关、距离变换、动态编程、结构匹配、链码相关等算法。

## 图像拼接技术

图像拼接分为四个步骤：图像匹配（registration）、重投影（reprojection）、缝合（stitching）和融合（blending）

- 图像匹配：是指一对描绘相同场景之间的几张图片的几何对应关系。一组照片可以是不同时间不同位置的拍摄，或者由多个传感器同时拍摄多张图像。
- 重投影：通过图像的几何变换，把一系列图片转换成一个共同的坐标系
- 缝合：通过合并重叠部分的像素值并保持没有重叠的像素值使之生成更大画布的图像
- 融合：通过几何和光度偏移错误通常导致对象的不连续，并在两个图像之间的边界附近产生可见的接缝。因此，为了减小接缝的出现，需要在缝合时或缝合之后使用混合算法.
