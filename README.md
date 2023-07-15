# MobileViTPose : Lightening of Human Pose Estimation Algorithm Using MobileViT and Transfer Learning

## Abstract
Transformer-based models, which have recently shown strength in the field of natural language processing, have also shown better performance than convolutional neural network-based models in the field of computer vision, increasing their influence. This is the same situation in the task of estimating human pose, and the appropriate example is that Vision Transformer-based ViTPose maintains the best performance in all human pose estimation benchmarks such as COCO, OCHuman, and MPII. However, because Vision Transformer has a heavy model structure with a large number of parameters and requires a relatively large amount of computation, it costs users a lot of money in learning. Therefore, this paper proposes a model that can perform human pose estimation tasks through a MobileViT-based model with fewer parameters and faster estimation. The proposed model is the Validation Set provided by the MS COCO human pose estimation benchmark, which showed 3.28GFLOPs and 9.72 million parameters of 1/5 and 1/9 compared to ViTPose, respectively, and showed relatively good performance by achieving 69.4 Mean Average Precision.


<img width="800" height="400" src="architecture.png"/>

## Results and Models
### Results on COCO val2017 on COCO val2017 dataset

| Model  | Backbone | #Params(M) | FLOPs(G) | Input Resolution | Feature Resolution | AP | AR |
| :----------------- | :-----------: | :------: | :-----------: | :------: |:------: | :------: | :------: | :------: | :------: |
| VGG | VGG16 | 19M | 16G | 256 x 192 | 1/4 | 69.8 | 75.4 | 
| SimpleBaseline | ResNet-50 | 34M | 9G | 256 x 192 | 1/4 | 70.4 | 76.3 | 
| SimpleBaseline | ResNet-152 | 69M | 16G | 256 x 192 | 1/4 | 72.0 | 77.8 | 
| HRNet | HRNet-W32 | 29M | 8G | 256 x 192 | 1/4 | 74.4 | 78.9 | 
| HRNet | HRNet-W32 | 29M | 8G | 384 x 288 | 1/4 | 75.8 | 81.0 | 
| HRNet | HRNet-w48 | 64M | 16G | 256 x 192 | 1/4 | 75.1 | 80.4 | 
| HRNet | HRNet-w48 | 64M | 16G | 384 x 288 | 1/4 | 76.3 | 81.2 | 
| VIRPose-B | ViT-B | 86M | 17G | 256 x 192 | 1/16 | 75.8 | 81.1 | 
| MobileViTPose-XXS | MobileViT-XXS | 4M | 2G | 256 x 192 | 1/4 | 61.7 | 67.9 | 
| MobileViTPose-S | MobileViT-S | 9M | 3G | 256 x 192 | 1/4 | 69.4 | 74.9 | 



