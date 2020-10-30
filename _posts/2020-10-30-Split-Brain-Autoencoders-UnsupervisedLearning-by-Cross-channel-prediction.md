---
title: "Split-Brain Autoencoders: Unsupervised Learning by Cross-Channel Prediction"
categories:
  - Paper review
tags:
  - Autoencoder
  - RGB-D
  - Grayscale
  - Prediction
  - classification
  - detection
  - segmentation
---

# Overall Summary
이미지를 두개의 채널 이미지로 나눠 Encoder에 각각이 서로를 predict하도록 학습시킴으로써 lable없이도 feature representation을 학습하는 방법을 제안하였다.
L(lightness)와 ab(color)로 나누거나 RGB와 Depth 이미지로 나눠 Encoder에 넣는데, Encoder dimension을 절반씩 나눠갖는다. 
loss는 classification, regression 중 하나를 골라 계산하였다. 
PASCAL dataset에서 classification은 20개 object binary decision을 진행하였고, Detection은 Fast R-CNN framework를 이용해서 bounding box 찾고, Segmentation은 pixel-wise labeling of object class 하는것이다. **Rescaling method를 사용하였다.**
(1) representation bottleneck(AE에서 trivial identity mapping 배우는걸 방지하려고)가 forced abstraction을 진행하느라 info가 많이 사라지는데 이모델은 그게 없어도 됨.
(2) input dropout으로 abstraction을 진행.
(3) large-scale raw image data에 적용가능하고 pre-trained on full input data.

# Strengths and weaknesses

Strength: channel을 다르게 함으로써 unsupervised learning을 가능하게 한것, 그러면서도 dimension을 늘리지 않은채로 성능을 높인것. colorization이 성능이 좋은만큼 이것도 좋다.
Weakness: TBA

# Comments
이게 classification task에서 제일 잘하고, detection task에선 "Learning features by watching objects move"가 더 잘해서.
과연 image sequence에서 유사한 image와 아닌 image들의 representation을 잘 뽑을 수 있을지 모르겠음. 같은 object가 등장하면 그냥 다 똑같은 representation으로 뽑힐 것 같기도 하고.
과연 object의 position에 대한 정보도 들어갈 것인가.
