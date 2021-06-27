# 👏 Survey of Deep Face Anti-spoofing 🔥

This is the official repository of **Deep Learning for Face Anti-Spoofing: A Survey**, a comprehensive survey 
of recent progress in deep learning methods for face anti-spoofing (FAS) as well as the datasets and protocols.


## Introduction
We present a comprehensive review of recent deep learning methods for face anti-spoofing (mostly from 2018 to 2021). It covers hybrid (handcrafted+deep), pure deep learning, and generalized learning based methods for monocular RGB face anti-spoofing. It also includes multi-modal learning based methods as well as specialized sensor based FAS. It also presents detailed comparision among publicly available datasets, together with several classical evaluation protocols.

🔔 We will update this page frequently~ :tada::tada::tada:

---
## Contents

- [Datasets](#data)
  - [Using commercial RGB camera](#data_RGB)
  - [With multiple modalities or specialized sensors](#data_Multimodal)
- [Deep FAS methods with commercial RGB camera](#methods_RGB)
  - [Hybrid (handcrafted + deep)](#hybrid)
  - [End-to-end binary cross-entropy supervision](#binary)
  - [Pixel-wise auxiliary supervision](#auxiliary)
  - [Generative model with pixel-wise supervision](#generative)
  - [Domain adaptation](#DA)
  - [Domain generalization](#DG)
  - [Zero/Few-shot learning](#zero-shot)
  - [Anomaly detection](#oneclass)
- [Deep FAS methods with advanced sensor](#methods_advanced)
  - [Learning upon specialized sensor](#sensor)
  - [Multi-modal learning](#multimodal)
  
---
  ![image](https://github.com/ZitongYu/DeepFAS/blob/main/Topology.png)   
  
---


<a name="data" />

### 1️⃣ Datasets

<a name="data_RGB" />

#### Datasets recorded with commercial RGB camera

| Dataset    | Year | #Live/Spoof | #Sub. |  Setup | Attack Types |
| --------   | -----    | -----  |  -----  | ----- |------------------------|
| [NUAA](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.607.5449&rep=rep1&type=pdf)   | 2010 | 5105/7509(I) | 15 |  N/R | Print(flat, wrapped)|
| [YALE Recaptured](https://www.ic.unicamp.br/~rocha/pub/papers/2011-icip-spoofing-detection.pdf)   | 2011 | 640/1920(I) | 10 |  50cm-distance from 3 LCD minitors | Print(flat) |
| [CASIA-MFSD](http://www.cbsr.ia.ac.cn/users/jjyan/ZHANG-ICB2012.pdf)   | 2012 | 150/450(V) | 50 |  7 scenarios and 3 image quality | Print(flat, wrapped, cut), Replay(tablet)|
| [REPLAY-ATTACK](http://publications.idiap.ch/downloads/papers/2012/Chingovska_IEEEBIOSIG2012_2012.pdf)   | 2012 | 200/1000(V) | 50 |  Lighting and holding | Print(flat), Replay(tablet, phone) |
| [Kose and Dugelay](https://ieeexplore.ieee.org/document/6595862)   | 2013 | 200/198(I) | 20 |  N/R | Mask(hard resin) |
| [MSU-MFSD](http://biometrics.cse.msu.edu/Publications/Face/WenHanJain_FaceSpoofDetection_TIFS15.pdf)   | 2014 | 70/210(V) | 35 |  Indoor scenario; 2 types of cameras | Print(flat), Replay(tablet, phone) |
| [UVAD](https://ieeexplore.ieee.org/document/7017526)   | 2015 | 808/16268(V) | 404 | Different lighting, background and places in two sections | Replay(monitor) |
| [REPLAY-Mobile](https://ieeexplore.ieee.org/document/7736936)   | 2016 | 390/640(V) | 40 |  5 lighting conditions | Print(flat), Replay(monitor) |
| [HKBU-MARs V2](https://link.springer.com/chapter/10.1007/978-3-319-46478-7_6)   | 2016 | 504/504(V) | 12 | 7 cameras from stationary and mobile devices and 6 lighting settings | Mask(hard resin) from Thatsmyface and REAL-f |
| [MSU USSA](https://ieeexplore.ieee.org/document/7487030)   | 2016 | 1140/9120(I) | 1140 |  Uncontrolled; 2 types of cameras | Print(flat), Replay(laptop, tablet, phone)|
| [SMAD](https://ieeexplore.ieee.org/document/7867821)   | 2017 | 65/65(V) | - |  Color images from online resources | Mask(silicone) |
| [OULU-NPU](https://ieeexplore.ieee.org/document/7961798)   | 2017 | 720/2880(V) | 55 |  Lighting & background in 3 sections | Print(flat), Replay(phone) |
| [Rose-Youtu](https://ieeexplore.ieee.org/document/8279564)   | 2018 | 500/2850(V) | 20 | 5 front-facing phone camera; 5 different illumination conditions | Print(flat), Replay(monitor, laptop),Mask(paper, crop-paper)|
| [SiW](https://arxiv.org/abs/1803.11097)   | 2018 | 1320/3300(V) | 165 |  4 sessions with variations of distance, pose, illumination and expression | Print(flat, wrapped), Replay(phone, tablet, monitor)|
| [WFFD](https://arxiv.org/abs/2005.06514)   | 2019 | 2300/2300(I) 140/145(V) | 745 |  Collected online; super-realistic; removed low-quality faces | Waxworks(wax)|
| [SiW-M](https://openaccess.thecvf.com/content_CVPR_2019/papers/Liu_Deep_Tree_Learning_for_Zero-Shot_Face_Anti-Spoofing_CVPR_2019_paper.pdf)   | 2019 | 660/968(V) | 493 |  Indoor environment with pose, lighting and expression variations | Print(flat), Replay, Mask(hard resin, plastic, silicone, paper, Mannequin), Makeup(cosmetics, impersonation, Obfuscation), Partial(glasses, cut paper)|
| [Swax](https://arxiv.org/abs/1910.09642)   | 2020 | Total 1812(I) 110(V) | 55 |  Collected online; captured under uncontrolled scenarios | Waxworks(wax)|
| [CelebA-Spoof](https://link.springer.com/chapter/10.1007/978-3-030-58610-2_5)   | 2020 | 156384/469153(I) | 10177 |  4 illumination conditions; indoor & outdoor; rich annotations | Print(flat, wrapped), Replay(monitor tablet, phone), Mask(paper)|
| [RECOD-Mtablet](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0238058)   | 2020 | 450/1800(V) | 45 | Outdoor environment and low-light & dynamic sessions | Print(flat), Replay(monitor) |
| [CASIA-SURF 3DMask](https://ieeexplore.ieee.org/document/9252183)   | 2020 | 288/864(V)  | 48 |  High-quality identity-preserved; 3 decorations and 6 environments | Mask(mannequin with 3D print) |
| [HiFiMask](https://arxiv.org/abs/2104.06148)   | 2021 | 13650/40950(V) | 75 |  three mask decorations; 7 recording devices; 6 lighting conditions; 6 scenes | Mask(transparent, plaster, resin)|




<a name="data_Multimodal" />

#### Datasets with multiple modalities or specialized sensors

| Dataset    | Year | #Live/Spoof | #Sub. |  M&H | Setup | Attack Types |
| --------   | -----    | -----  |  -----  | -----  | -----  |------------------------|
| [3DMAD](https://ieeexplore.ieee.org/document/6810829)   | 2013 | 170/85(V) | 17 |  VIS, Depth | 3 sessions (2 weeks interval) | Mask(paper, hard resin)|
| [GUC-LiFFAD](https://ieeexplore.ieee.org/document/7018027)   | 2015 | 1798/3028(V) | 80 |  Light field | Distance of 1.5 constrained conditions | Print(Inkjet paper, Laserjet paper), Replay(tablet)|
| [3DFS-DB](https://www.researchgate.net/publication/277905873_Three-dimensional_and_two-and-a-half-dimensional_face_recognition_spoofing_using_three-dimensional_printed_models)   | 2016 | 260/260(V) | 26 |  VIS, Depth | Head movement with rich angles | Mask(plastic)|
| [BRSU Skin/Face/Spoof](https://ieeexplore.ieee.org/document/7550052)   | 2016 | 102/404(I) | 137 |  VIS, SWIR | multispectral SWIR with 4 wavebands 935nm, 1060nm, 1300nm and 1550nm | Mask(silicon, plastic, resin, latex)|
| [Msspoof](https://link.springer.com/chapter/10.1007/978-3-319-28501-6_8)   | 2016 | 1470/3024(I) | 21 |  VIS, NIR | 7 environmental conditions | Black&white Print(flat) |
| [MLFP](https://ieeexplore.ieee.org/document/8014774)   | 2017 | 150/1200(V) | 10 |  VIS, NIR, Thermal | Indoor and outdoor with fixed and random backgrounds | Mask(latex, paper) |
| [ERPA](https://www.researchgate.net/publication/320177829_What_You_Can't_See_Can_Help_You_-_Extended-Range_Imaging_for_3D-Mask_Presentation_Attack_Detection)   | 2017 | Total 86(V) | 5 |  VIS, Depth, NIR, Thermal | Subject positioned close (0.3∼0.5m) to the 2 types of cameras | Print(flat), Replay(monitor), Mask(resin, silicone) |
| [LF-SAD ](http://www.ee.cityu.edu.hk/~lmpo/publications/2019_JEI_Face_Liveness.pdf)   | 2018 | 328/596(I) | 50 |  Light field | Indoor fix background, captured by Lytro ILLUM camera | Print(flat, wrapped), Replay(monitor) |
| [CSMAD](https://ieeexplore.ieee.org/document/8698550)   | 2018 | 104/159(V+I) | 14 |  VIS, Depth, NIR, Thermal | 4 lighting conditions | Mask(custom silicone) |
| [3DMA](https://ieeexplore.ieee.org/document/8909845)   | 2019 | 536/384(V) | 67 |  VIS, NIR | 48 masks with different ID; 2 illumination & 4 capturing distances | Mask(plastics) |
| [CASIA-SURF](https://openaccess.thecvf.com/content_CVPR_2019/papers/Zhang_A_Dataset_and_Benchmark_for_Large-Scale_Multi-Modal_Face_Anti-Spoofing_CVPR_2019_paper.pdf)   | 2019 | 3000/18000(V) | 1000 |  VIS, Depth, NIR | Background removed; Randomly cut eyes, nose or mouth areas | Print(flat, wrapped, cut) |
| [WMCA](https://ieeexplore.ieee.org/document/8714076)   | 2019 | 347/1332(V) | 72 |  VIS, Depth, NIR, Thermal | 6 sessions with different backgrounds and illumination; pulse data for bonafide recordings | Print(flat), Replay(tablet), Partial(glasses), Mask(plastic, silicone, and paper, Mannequin) |
| [CeFA](https://openaccess.thecvf.com/content/WACV2021/html/Liu_CASIA-SURF_CeFA_A_Benchmark_for_Multi-Modal_Cross-Ethnicity_Face_Anti-Spoofing_WACV_2021_paper.html)   | 2020 | 6300/27900(V) | 1607 |  VIS, Depth, NIR | 3 ethnicities; outdoor & indoor; decoration with wig and glasses | Print(flat, wrapped), Replay, Mask(3D print, silica gel) |
| [HQ-WMCA](https://ieeexplore.ieee.org/abstract/document/9146362)   | 2020 | 555/2349(V) | 51 | VIS, Depth, NIR, SWIR, Thermal | Indoor; 14 ‘modalities’, including 4 NIR and 7 SWIR wavelengths; masks and mannequins were heated up to reach body temperature | Laser or inkjet Print(flat), Replay(tablet, phone), Mask(plastic, silicon, paper, mannequin), Makeup, Partial(glasses, wigs, tatoo) |




---
<a name="methods_RGB" />

### 2️⃣ Deep FAS methods with commercial RGB camera

- temp

<a name="hybrid" />

#### Hybrid (handcrafted + deep)

| Method    | Year | Backbone | Loss |  Input | Static/Dynamic |
| --------   | -----    | -----  |  -----  | -----  | -----  |
| [DPCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2016 | VGG-Face | Trained with SVM |  RGB | S|
| [Multi-cues+NN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2016 | MLP | Binary CE loss |  RGB+OFM | D|
| [CNN LBP-TOP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2017 | 5-layer CNN | Binary CE loss, SVM |  RGB | D|
| [DF-MSLBP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | Deep forest | Binary CE loss |  HSV+YCbCr | S|
| [SPMT+SSD](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | VGG16 | Binary CE loss, SVM, bbox regression |  RGB, Landmarks | S|
| [CHIF](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | VGG-Face | Trained with SVM |  RGB | S|
| [DeepLBP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | VGG-Face | Binary CE loss, SVM |  RGB, HSV, YCbCr | S|
| [CNN+LBP+WLD](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | CaffeNet | Binary CE loss |  RGB | S|
| [Intrinsic](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | 1D-CNN | Trained with SVM |  Reflection | D|
| [FARCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Multi-scale attentional CNN | Regression loss, Crystal loss, Center loss |  RGB | S|
| [CNN-LSP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | 1D-CNN | Trained with SVM |  RGB | D |
| [DT-Mask](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | VGG16 | Binary CE loss, Channel&Spatial discriminability |  RGB+OF | D |
| [VGG+LBP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | VGG16 | Binary CE loss |  RGB | S|
| [CNN+OVLBP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | VGG16 | Binary CE loss, NN classifier |  RGB | S|
| [HOG-Pert.](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Multi-scale CNN | Binary CE loss |  RGB+HOG | S|
| [LBP-Pert.](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Multi-scale CNN | Binary CE loss |  RGB+LBP | S|
| [TransRPPG](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | Vision Transformer | Binary CE loss |  rPPG map | D |



<a name="binary" />

#### End-to-end binary cross-entropy supervision
| Method    | Year | Backbone | Loss |  Input | Static/Dynamic |
| --------   | -----    | -----  |  -----  | -----  | -----  |
| [CNN1](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2014 | 8-layer CNN | Trained with SVM |  RGB | S|
| [LSTM-CNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2015 | CNN+LSTM | Binary CE loss |  RGB | D|
| [SpoofNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2015 | 2-layer CNN | Binary CE loss |  RGB | S|
| [HybridCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2017 | VGG-Face | Trained with SVM |  RGB | S|
| [CNN2](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2017 | VGG11 | Binary CE loss |  RGB | S|
| [Ultra-Deep](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2017 | ResNet50+LSTM | Binary CE loss |  RGB | D|
| [FASNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2017 | VGG16 | Binary CE loss |  RGB | S|
| [CNN3](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | Inception, ResNet | Binary CE loss |  RGB | S|
| [MILHP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | ResNet+STN | Multiple Instances CE loss |  RGB | D|
| [LSCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | 9 PatchNets | Binary CE loss |  RGB | S|
| [LiveNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | VGG11 | Binary CE loss |  RGB | S|
| [MS-FANS ](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | AlexNet+LSTM | Binary CE loss |  RGB | S|
| [DeepColorFAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | 5-layer CNN | Binary CE loss |  RGB, HSV, YCbCr | S|
| [Siamese](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | AlexNet | Contrastive loss |  RGB | S|
| [FSBuster](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet50 | Trained with SVM |  RGB | S|
| [FuseDNG](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | 7-layer CNN | Binary CE loss, Reconstruction loss |  RGB | S|
| [STASN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet50+LSTM | Binary CE loss |  RGB | D|
| [TSCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet18 | Binary CE loss |  RGB, MSR | S|
| [FAS-UCM](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | MobileNetV2, VGG19 | Binary CE loss, Style loss |  RGB | S|
| [SLRNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet50+LSTM | Binary CE loss |  RGB | D|
| [GFA-CNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | VGG16 | Binary CE loss |  RGB | S|
| [3DSynthesis](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet15 | Binary CE loss |  RGB | S|
| [CompactNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | VGG19 | Points-to-Center triplet loss |  RGB | S|
| [SSR-FCN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | FCN with 6 layers | Binary CE loss |  RGB | S|
| [FasTCo](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet50 or MobileNetV2 | Multi-class CE loss, Temporal Consistency loss, Class Consistency loss|  RGB | D|
| [DRL-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18+GRU | Binary CE loss |  RGB | S|
| [SfSNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | 6-layer CNN | Binary CE loss |  Albedo, Depth, Reflection| S|
| [LivenesSlight](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | 6-layer CNN | Binary CE loss |  RGB | S|
| [MotionEnhancement](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | VGGface+LSTM | Binary CE loss |  RGB | D|
| [CFSA-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Binary CE loss |  RGB | S|
| [MC-FBC](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | VGG16, ResNet50 | Binary CE loss |  RGB | S|
| [SimpleNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Multi-stream 5-layer CNN | Binary CE loss |  RGB, OF, RP | D|
| [PatchCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | SqueezeNet v1.1 | Binary CE loss, Triplet loss |  RGB | S|
| [FreqSpatialTempNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Binary CE loss |  RGB, HSV, Spectral | D|
| [ViTranZFAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Vision Transformer | Binary CE loss |  RGB | S|
| [CIFL](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | ResNet18 | Binary focal loss, camear type loss |  RGB | S|






<a name="auxiliary" />

#### Pixel-wise auxiliary supervision

| Method    | Year | Supervision | Backbone |  Input | Static/Dynamic |
| --------   | -----    | -----  |  -----  | -----  | -----  |
| [Depth&Patch](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2017 | Depth | PatchNet, DepthNet |  YCbCr, HSV | S|
| [Auxiliary](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | Depth, rPPG spectrum | DepthNet |  RGB, HSV | D|
| [BASN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Depth, Reflection | DepthNet, Enrichment |  RGB, HSV | S|
| [DTN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | BinaryMask | Tree Network |  RGB, HSV | S|
| [PixBiS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | BinaryMask | DenseNet161 |  RGB | S|
| [A-PixBiS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask | DenseNet161 |  RGB | S|
| [Auto-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask | NAS |  RGB | S|
| [MRCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask | Shallow CNN |  RGB | S|
| [FCN-LSA](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask | DepthNet |  RGB | S|
| [CDCN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Depth | DepthNet |  RGB | S|
| [FAS-SGTD](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Depth | DepthNet, STPM |  RGB | D|
| [TS-FEN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Depth | ResNet34, FCN |  RGB, YCbCr, HSV | S|
| [SAPLC](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | TernaryMap | DepthNet |  RGB, HSV | S|
| [BCN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask, Depth, Reflection | DepthNet |  RGB | S|
| [Disentangled](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Depth, TextureMap | DepthNet |  RGB | S|
| [AENet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Depth, Reflection | ResNet18 |  RGB | S|
| [3DPC-Net](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | 3D Point Cloud | ResNet18 |  RGB | S|
| [PS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask or Depth | ResNet50 or CDCN |  RGB | S|
| [NAS-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask or Depth | NAS |  RGB | D|
| [DAM](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | Depth | VGG16, TSM |  RGB | D|
| [Bi-FPNFAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | Fourier spectra | EfficientNetB0, FPN |  RGB | S|
| [DC-CDN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | Depth | CDCN |  RGB | S|



<a name="generative" />

#### Generative model with pixel-wise supervision

| Method    | Year | Supervision | Backbone |  Input | Static/Dynamic |
| --------   | -----    | -----  |  -----  | -----  | -----  |
| [De-Spoof](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | Depth, BinaryMask, FourierMap | DSNet, DepthNet |  RGB, HSV | S|
| [Reconstruction](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | RGB Input (live), ZeroMap (spoof) | U-Net |  RGB | S|
| [LGSC](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ZeroMap (live) | U-Net, ResNet18 |  RGB | S|
| [TAE](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Binary CE loss, Reconstruction loss | Info-VAE, DenseNet161 |  RGB | S|
| [STDN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | BinaryMask, RGB Input (live) | U-Net, PatchGAN |  RGB | S|
| [GOGen](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | RGB input |  DepthNet |  RGB+one-hot vector | S|
| [PhySTD](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | Depth, RGB Input (live) |  U-Net, PatchGAN |  Frequency Trace | S|
| [MT-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | ZeroMap (live), LearnableMap (Spoof) |  DepthNet |  RGB | S|



<a name="DA" />

#### Domain adaptation

| Method    | Year | Backbone | Loss |  Static/Dynamic |
| --------   | -----    | -----  |  -----  | -----  | 
| [OR-DA](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | AlexNet | Binary CE loss, MMD loss |  S|
| [DTCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | AlexNet | Binary CE loss, MMD loss |  S|
| [Adversarial](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet18 | Triplet loss, Adversarial loss |  S|
| [ML-MMD](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Multi-scale FCN | CE loss, MMD loss |  S|and unlabeled sets
| [OCA-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | DepthNet | Binary CE loss, Pixel-wise binary loss |  S|
| [DR-UDA](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Center&Triplet loss, Adversarial loss, Disentangled loss |  S|
| [DGP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | DenseNet161 | Feature divergence measure, BinaryMask loss |  S|
| [Distillation](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | AlexNet | Binary CE loss, MMD loss , Paired Similarity |  S|
| [S-CNN++PL+TC](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | ResNet18 | CE Loss in labeled and unlabeled sets |  D|
| [USDAN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | ResNet18 | Adaptive binary CE loss, Entropy loss, Adversarial loss |  S|





<a name="DG" />

#### Domain generalization


| Method    | Year | Backbone | Loss |  Static/Dynamic |
| --------   | -----    | -----  |  -----  | -----  | 
| [MADDG](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | DepthNet | Binary CE & Depth loss, Multi-adversarial loss, Dual-force Triplet loss |  S|
| [PAD-GAN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Binary CE & Depth loss, Multi-adversarial loss, Dual-force Triplet loss |  S|
| [DASN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Binary CE & Spoof-irrelevant factor loss |  S|
| [SSDG](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Binary CE loss, Single-Side adversarial loss, Asymmetric Triplet loss |  S|
| [RF-Meta](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | DepthNet | Binary CE loss, Depth loss |  S|
| [CCDD](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet50+LSTM | Binary CE loss, Class-conditional loss |  D|
| [SDA](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | DepthNet | Binary CE & Depth loss, Reconstruction loss, Orthogonality regularization |  S|
| [D2AM](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | DepthNet | Binary CE loss, Depth loss, MMD loss |  S|




<a name="zero-shot" />

#### Zero/Few-shot learning


| Method    | Year | Backbone | Loss |  Input |
| --------   | -----    | -----  |  -----  | -----  | 
| [DTN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Deep Tree Network | Binary CE loss, Pixel-wise binary loss, Unsupervised Tree loss |  RGB, HSV|
| [AIM-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | DepthNet | Depth loss, Contrastive Depth loss |  RGB |
| [CM-PAD](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | DepthNet, ResNet | Binary CE loss, Depth loss, Gradient alignment |  RGB|



<a name="oneclass" />

#### Anomaly detection


| Method    | Year | Backbone | Loss |  Input |
| --------   | -----    | -----  |  -----  | -----  | 
| [AE+LBP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2018 | AutoEncoder | Reconstruction loss |  RGB|
| [Anomaly](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet50 | Triplet focal loss, Metric-Softmax loss |  RGB|
| [Anomaly2](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | GoogLeNet or ResNet50 | Mahalanobis distance |  RGB|
| [Hypersphere](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Hypersphere loss |  RGB, HSV |
| [Ensemble-Anomaly](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | GoogLeNet or ResNet50 | Gaussian Mixture Model (not end-to-end) |  RGB, patches|
| [MCCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | LightCNN | Binary CE loss, Contrastive loss |  Grayscale, IR, Depth, Thermal|
| [End2End-Anomaly](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | VGG-Face | Binary CE loss, Pairwise confusion |  RGB|
| [ClientAnomaly](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet50 or GoogLeNet or VGG16 | One-class SVM or Mahalanobis distance or Gaussian Mixture Model |  RGB|







---
<a name="methods_advanced" />

### 3️⃣ Deep FAS methods with advanced sensor


<a name="sensor" />

#### Learning upon specialized sensor


| Method    | Year | Backbone | Loss |  Input | Static/Dynamic |
| --------   | -----    | -----  |  -----  | -----  | -----  |
| [Thermal-FaceCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | AlexNet | Regression loss |  Thermal infrared face image | S|
| [SLNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | 17-layer CNN | Binary CE loss |  Stereo (left&right) face images | S|
| [Aurora-Guard](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | U-Net | Binary CE loss, Depth regression, Light Regression |  Casted face with dynamic changing light specified by random light CAPTCHA | D|
| [LFC](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | AlexNet | Binary CE loss |  Ray difference/microlens images from light field camera | S|
| [PAAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | MobileNetV2 | Contrastive loss, SVM |  Four-directional polarized face image | S|
| [Face-Revelio](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Siamese-AlexNet | L1 distance |  Four flash lights displayed on four quarters of a screen | D|
| [SpecDiff](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet4 | Binary CE loss |  Concatenated face images w/ and w/o flash | S|
| [MC-PixBiS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | DenseNet161 | Binary mask loss |  SWIR images differences | S|
| [Thermalization](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | YOLO V3+GoogLeNet | Binary CE loss |  Thermal infrared face image | S|
| [DP Bin-Cls-Net](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | Shallow U-Net + Xception | Transformation consistency, Relative disparity loss, Binary CE loss |  DP image pair | S|





<a name="multimodal" />

#### Multi-modal learning

| Method    | Year | Backbone | Loss |  Input | Fusion |
| --------   | -----    | -----  |  -----  | -----  | -----  |
| [FaceBagNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Multi-stream CNN | Binary CE loss |  RGB, Depth, NIR face patches | Feature-level|
| [FeatherNets](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Ensemble-FeatherNet | Binary CE loss |  Depth, NIR | Decision-level |
| [Attention](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet18 | Binary CE loss, Center loss |  RGB, Depth, NIR | Feature-level|
| [mmfCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet34 | Binary CE loss, Binary Center Loss | RGB, NIR, Depth, HSV, YCbCr | Feature-level|
| [MM-FAS](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet18/50 | Binary CE loss |  RGB, NIR, Depth | Feature-level|
| [AEs+MLP](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | Autoencoder, MLP | Binary CE loss, Reconstruction loss |  Grayscale-Depth-Infrared composition| Input-level|
| [SD-Net](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | ResNet18 | Binary CE loss |  RGB, NIR, Depth | Feature-level|
| [Dual-modal](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2019 | MoblienetV3 | Binary CE loss |  RGB, IR | Feature-level|
| [Parallel-CNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Attentional CNN | Binary CE loss |  Depth, NIR | Feature-level|
| [Multi-Channel Detector](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | RetinaNet (FPN+ResNet18) | Landmark regression, Focal loss |  Grayscale-Depth-Infrared composition | Input-level|
| [PSMM-Net](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | ResNet18 | Binary CE loss for each stream |  RGB, Depth, NIR | Feature-level|
| [PipeNet](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | SENet154 | Binary CE loss |  RGB, Depth, NIR face patches | Feature-level|
| [MM-CDCN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | CDCN | Pixel-wise binary loss, Contrastive depth loss |  RGB, Depth, NIR | Feature&Decision-level|
| [HGCNN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | Hypergraph-CNN, MLP | Binary CE loss |  RGB, Depth | Feature-level|
| [MCT-GAN](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2020 | CycleGAN, ResNet50 | GAN loss, Binary CE loss |  RGB, NIR | Input-level|
| [D-M-Net](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | ResNeXt | Binary CE loss |  Multi-preprocessed Depth, RGB-NIR composition | Input&Feature-level|
| [CMFL](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | DenseNet161 | Binary CE loss, Cross modal focal loss |  RGB, Depth | Feature-level|
| [MA-Net](https://openaccess.thecvf.com/content_CVPR_2020/papers/Yu_Searching_Central_Difference_Convolutional_Networks_for_Face_Anti-Spoofing_CVPR_2020_paper.pdf)   | 2021 | CycleGAN, ResNet18 | Binary CE loss, GAN loss |  RGB, NIR | Feature-level|








---

### Citation
If you find our work useful in your research, please consider citing:

    @article{yu2021deep,
      title={Deep Learning for Face Anti-Spoofing: A Survey},
      author={Yu, Zitong and Qin, Yunxiao and Li, Xiaobai and Zhao, Chenxu and Lei, Zhen and Zhao, Guoying},
      journal={arXiv},
      year={2021}
    }
    
