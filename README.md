# super_resolution_paper_lists
reading paper lists of super resolution

# [Real-Time Single Image and Video Super-Resolution Using an Efficient Sub-Pixel Convolutional Neural Network](https://arxiv.org/pdf/1609.05158.pdf)
论文链接：https://arxiv.org/pdf/1609.05158.pdf
超分任务，将低分辨率空间映射到高分辨率空间是必要操作。
  * 前人采用的很多方法，如在网络前/中/后分别提升图像分辨率，一方面，增强之前上采样将提升分辨率；另一方面，直接使用bicubic的上采样方法没有引入额外的信息解决病态问题。
  * 通过学习的方式实现上采样被广泛认为是更好的方式，然而却缺乏有效的提升分辨率的卷积层。
  * 因此，文章提出一种有效的亚像素卷积方法，其实就是类似于以channel维度换取空间维度的方法，在最后一层估计的channel数目为上采样倍率的平方数scale^2，最后通过有偏移的叠加每一个维度获取高分辨率结果。
（PS：其实非常类似于多帧超分的原理，以2倍上采样为例，4帧图像若刚好为真实世界上下左右各偏移一个像素的结果，则可以直接还原出高分辨率结果）
