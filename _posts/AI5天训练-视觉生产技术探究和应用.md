---
layout:     post
title:      阿里云-AI五天实践（第一天）
subtitle:   视觉生产技术探究和应用
date:       2020-05-16
author:     涂诣
header-img: img/post-bg-j.jpg
catalog: true
tags:
    - AI
---

# 视觉生产技术探究和应用

## 概念理解

 ### 定义

![image-20200516154422018](https://i.loli.net/2020/05/16/36zN15ohjmG7tVc.png)

通过一个或一系列视觉过程，产出新的视觉表达，是人或机器能够感知的图像视频，而不是标签或特征。

### 分类

- 生成:从0到1

- 拓展:从1到N

- 摘要:从N到1

- 升维:从An到An+ 1 

- 增强/变换：从A到B

- 插入/合成：A+B=C

- 擦除：A-B=C

### 通用基础框架

![通用基础框架](https://i.loli.net/2020/05/16/2srpnjEDQYUeKcW.png)



### 五个关键维度

1.可看（满足视觉/美学表现）

2.合理（合乎语义/内容逻辑）

3.多样（保证结果的丰富性）

4.可控（提供用户预期的抓手）

5.可用（带来用户/商业价值）

![五个关键维度](https://i.loli.net/2020/05/16/c3F8vd4WweYAEC1.png)

## 精细理解

### 分割抠图

1. 识别：能知道图片中物体，知道物体是什么。
2. 检测：能识别，还要能知道在哪个区域。
3. 分割：识别、检测、并知道每一个像素是什么，能将区域完整切割分离。

**难点**

1. 复杂背景

2. 遮挡

3. 发丝精抠（图像中毛发等细微处

4. 边缘反色

5. 透明材质（图像中玻璃等

6. 多尺度/目标

7. 数据严重不足，标注成本高

**解题思路**
Semantic Segmentation（语义分割）

Instance Segmentation（实例分割）

Image Matting（抠图）

![image-20200516164333882](https://i.loli.net/2020/05/16/mWEiyp6MoFZ9u5K.png)

**思路**：1.复杂问题拆解：粗mask估计+精准matting
		2.丰富数据样本：设计图像mask统一模型

**模型框架**  

Step1：mask粗分割

Step2：mask质量统一

Step3：估计精确alpha

![Snipaste_2020-05-16_17-34-26](https://i.loli.net/2020/05/16/Wbrn9UT6QO1EXm3.jpg)

## 视觉生成
### 框架流程

1.理需求

2.定草图

3.选状态

4.调细节

5.生成图

6.评好坏

## 视觉编辑
 **视频植入作用**

- 挖掘视频核心价值

- 扩大植入覆盖范围

- 提升植入效果效率

![Clip_20200516_171808](https://i.loli.net/2020/05/16/tGvcrMdzia9Ff2X.png)

![Clip_20200516_171855](https://i.loli.net/2020/05/16/Pdg1O5IqQNZ8tJC.png)

### 关键点

（广告等）植入位检测与定位

动态检测分割

视频内容擦除

文字擦除

Logo擦除

画幅变化（缩放

图像尺寸变化

## 视觉增强

- 视频增强

- 人脸修复增强

- 渲染图超分

- 视频插帧

- HDR色彩扩展

- 风格迁移

- 颜色拓展

![Clip_20200516_172232](https://i.loli.net/2020/05/16/hCqQlw32XAzk6Jo.png)

## 视觉制造

### 实体设计制造

**缺点**

- 效率低：多次打样，多次沟通（服装设计平均30天）

- 协同差：设计、营销、生成脱节、倒置

- 定制难：无法实现柔性生产

**核心逻辑**

![Clip_20200516_172437](https://i.loli.net/2020/05/16/AxluG6Q2rNPeY8B.png)

**包装几何生成**

![Clip_20200516_172722](https://i.loli.net/2020/05/16/d1sDiKPCYypabwz.png)

**服装几何生成**

![Clip_20200516_172737](https://i.loli.net/2020/05/16/U2JqYC3MTzdtH6L.png)

**材质工艺**

![Clip_20200516_172803](https://i.loli.net/2020/05/16/Nhg1QObPErmqYKn.png)

**多样性拓展**

![Clip_20200516_172818](https://i.loli.net/2020/05/16/qQhCBbovOIAaS9m.png)

**2D3D融合**

![Clip_20200516_172839](https://i.loli.net/2020/05/16/85g3jyMFAeTWufO.png)

## 应用平台

### 鹿班

鹿班是视觉生成领域在业界落地的先行者，对外提供大规模在线的AI设计服务

![Clip_20200516_173139](https://i.loli.net/2020/05/16/mychns2AGCRQF7B.png)

### AlibabaWood

AI生成商品短视频，能做到剧本生成、智能文案生成、自动剪辑、智能音乐推荐。

### 阿里云视觉开放平台

提供高易用、普惠的视觉API服务