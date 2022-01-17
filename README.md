# super_resolution_paper_lists
reading paper lists of super resolution

# Up-sample operation
## [Real-Time Single Image and Video Super-Resolution Using an Efficient Sub-Pixel Convolutional Neural Network](https://arxiv.org/pdf/1609.05158.pdf)

论文链接：https://arxiv.org/pdf/1609.05158.pdf

超分任务，将低分辨率空间映射到高分辨率空间是必要操作。
  * 前人采用的很多方法，如在网络前/中/后分别提升图像分辨率，一方面，增强之前上采样将提升分辨率；另一方面，直接使用bicubic的上采样方法没有引入额外的信息解决病态问题。
  * 通过学习的方式实现上采样被广泛认为是更好的方式，然而却缺乏有效的提升分辨率的卷积层。
  * 因此，文章提出一种有效的亚像素卷积方法，其实就是类似于以channel维度换取空间维度的方法，在最后一层估计的channel数目为上采样倍率的平方数scale^2，最后通过有偏移的叠加每一个维度获取高分辨率结果。
（PS：其实非常类似于多帧超分的原理，以2倍上采样为例，4帧图像若刚好为真实世界上下左右各偏移一个像素的结果，则可以直接还原出高分辨率结果）

# Single image super resolution
## [2016 CVPR Accurate Image Super-Resolution Using Very Deep Convolutional Networks](https://openaccess.thecvf.com/content_cvpr_2016/papers/Kim_Accurate_Image_Super-Resolution_CVPR_2016_paper.pdf)
论文链接：https://openaccess.thecvf.com/content_cvpr_2016/papers/Kim_Accurate_Image_Super-Resolution_CVPR_2016_paper.pdf
早期基于深度学习的图像超分辨方法，针对SRCNN提出改进
1）感受野：文章提出深的网络结构提升感受野，并证明 the deeper, the better
2) 收敛性：增大学习率，提升收敛速度
3）超分因子：输入上插为目标分辨率，混合多个超分因子进行训练

# Multi-frame image super resolution(including video)
### Introduction:
Multi-frame image super-resolution algorithms based on deep learning almost include (feature extraction) alignment, fusion, and reconstruction, which are similar to traditional multi-frame methods consisting of alignment, fusion, and post-process. Due to the different alignment methods, there are two categories, including: 
* implicitly align methods based on deformable convolutional network; 
* explicitly align methods based on optical flow. It needs additional supervision or pretraining on other tasks
## [2019 CVPR EDVR: Video Restoration with Enhanced Deformable Convolutional Networks](https://openaccess.thecvf.com/content_CVPRW_2019/papers/NTIRE/Wang_EDVR_Video_Restoration_With_Enhanced_Deformable_Convolutional_Networks_CVPRW_2019_paper.pdf)

论文链接：https://openaccess.thecvf.com/content_CVPRW_2019/papers/NTIRE/Wang_EDVR_Video_Restoration_With_Enhanced_Deformable_Convolutional_Networks_CVPRW_2019_paper.pdf

经典的视频超分方法，在NTIRE19 video restoration and enhancement challenges获得冠军。包括对齐、融合、重建三个部分。
* **输入**：当前帧，前N帧，后N帧，共2N+1帧
* **对齐方法**：金字塔式级联的可行变卷积网络实现隐式对齐。采用stride conv 下采样，每个level 都经过DCN(deformable convolution network),得到该level的feature 和offset，通过bilinear分别对feature和offset上采样给下一层使用.
* **融合方法**：时空注意力机制。融合的目标， 一方面是克服相邻帧之间存在的遮挡、模糊和视差问题；另一方面是避免误对齐对后续的影响。因此评估待融合帧和参考帧之间的相似性是融合的关键。时域上，在特征中间计算每一帧相对参考帧的融合权重，根据权重进行融合；空域上，采用金字塔设计提升开给你剪感受野。
* **重建**： 两阶段复原。级联一个轻量化版本的EDVR，用于解决严重的运动模糊并减轻输出帧的不一致性
