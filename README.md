# MobileViTPose : Lightening of Human Pose Estimation Algorithm Using MobileViT and Transfer Learning

## Abstract
Transformer-based models, which have recently shown strength in the field of natural language processing, have also shown better performance than convolutional neural network-based models in the field of computer vision, increasing their influence. This is the same situation in the task of estimating human pose, and the appropriate example is that Vision Transformer-based ViTPose maintains the best performance in all human pose estimation benchmarks such as COCO, OCHuman, and MPII. However, because Vision Transformer has a heavy model structure with a large number of parameters and requires a relatively large amount of computation, it costs users a lot of money in learning. Therefore, this paper proposes a model that can perform human pose estimation tasks through a MobileViT-based model with fewer parameters and faster estimation. The proposed model is the Validation Set provided by the MS COCO human pose estimation benchmark, which showed 3.28GFLOPs and 9.72 million parameters of 1/5 and 1/9 compared to ViTPose, respectively, and showed relatively good performance by achieving 69.4 Mean Average Precision.


<img width="800" height="400" src="architecture.png"/>

## Results and Models
### Results on COCO val2017 on COCO val2017 dataset

| Model  | Backbone | #Params(M) | FLOPs(G) | Input Resolution | Feature Resolution | AP | AR |
| :----------------- | :-----------: | :------: | :-----------: | :------: |:------: | :------: | :------: | :------: | :------: |
| VGG  | VGG16 | 19M | 16G | 0.628 | 256 x 192 | 1/4 | 69.8 | 75.4 | 
| [Wider Naive Lite-HRNet-18](/configs/top_down/naive_litehrnet/coco/wider_naive_litehrnet_18_coco_256x192.py)  | 256x192 | 1.3M | 311.1M | 0.660 | 0.871 | 0.737 | 0.721 | 0.913 | [GoogleDrive](https://drive.google.com/file/d/1Amb0yE677zV18KaH6gruUQnHUiwBx_-H/view?usp=sharing) or [OneDrive](https://1drv.ms/u/s!AvreNzlRJaHngQLsLGlp3r16ALfZ?e=XgMYMd) |
| [Lite-HRNet-18](/configs/top_down/lite_hrnet/coco/litehrnet_18_coco_256x192.py)  | 256x192 | 1.1M | 205.2M |0.648 | 0.867 | 0.730 | 0.712 | 0.911 | [GoogleDrive](https://drive.google.com/file/d/1ZewlvpncTvahbqcCFb-95C3NHet30mk5/view?usp=sharing) or [OneDrive](https://1drv.ms/u/s!AvreNzlRJaHngQE0r-EVnMNPObk7?e=ojJosi) |
| [Lite-HRNet-18](/configs/top_down/lite_hrnet/coco/litehrnet_18_coco_384x288.py)  | 384x288 | 1.1M | 461.6M | 0.676 | 0.878 | 0.750 | 0.737 | 0.921 | [GoogleDrive](https://drive.google.com/file/d/1E3S18YbUfBm7YtxYOV7I9FmrntnlFKCp/view?usp=sharing) or [OneDrive](https://1drv.ms/u/s!AvreNzlRJaHnfZE0w9s_h9oK98c?e=xPiAxS) |
| [Lite-HRNet-30](/configs/top_down/lite_hrnet/coco/litehrnet_30_coco_256x192.py)  | 256x192 | 1.8M | 319.2M | 0.672 | 0.880 | 0.750 | 0.733 | 0.922 | [GoogleDrive](https://drive.google.com/file/d/1KLjNInzFfmZWSbEQwx-zbyaBiLB7SnEj/view?usp=sharing) or [OneDrive](https://1drv.ms/u/s!AvreNzlRJaHnexxp5RCK15meEWw?e=g4ObHb) |
| [Lite-HRNet-30](/configs/top_down/lite_hrnet/coco/litehrnet_30_coco_384x288.py)  | 384x288 | 1.8M | 717.8M | 0.704 | 0.887 | 0.777 | 0.762 | 0.928 | [GoogleDrive](https://drive.google.com/file/d/1BcHnLka4FWiXRmPnJgJKmsSuXXqN4dgn/view?usp=sharing) or [OneDrive](https://1drv.ms/u/s!AvreNzlRJaHnfOng41YajWZg478?e=wVKeIS) |
