# Construction of Semantic Topological Map for Domestic Environment
#### 成员：张嘉浩，叶蔚林，徐璐
#### 内容：面向家具环境的语义拓扑地图的构建
---
#### 环境配置：
- Anaconda3

- python3.6 / 3.7

- pycharm (IDE)

- pytorch 1.6 (pip package)

- torchvision 0.7.0 (pip package)

- tensorflow 2.4 (pip package)

  

#### 面向家居环境：

1. 建立主体
   1. 遍历`[class_ids]`，检测桌子，椅子等物品
   2. 检测到桌子->将桌子设置为主体，等
      1. 如果有两张及以上桌子，选取`[roi]`最大的为主体
2. 遍历`[rois]`，与主体`[roi]`进行比较
   1. `[rois]`与主体`[roi]`无重合：通过`[rois]`的相对位置（左/右）将物体归为主体左/右
   2. `[rois]`与主体`[roi]`有重合：
      1. 完全重叠，即`[rois]`在桌子`[roi]`内部：前/上
      2. 部分重叠，通过`[mask]`与`[rois]`判断遮挡关系：被遮挡的在后/下
3. 将关系设置为`.svg`文件
4. 画出拓扑地图



注：遮挡关系的判断，通过检测框与Mask的最边缘像素差值进行比较，差值大于某一个值，则说明该物体被遮挡
