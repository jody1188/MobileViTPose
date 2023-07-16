# MobileViTPose : Lightening of Human Pose Estimation Algorithm Using MobileViT and Transfer Learning

## Abstract
Transformer-based models, which have recently shown strength in the field of natural language processing, have also shown better performance than convolutional neural network-based models in the field of computer vision, increasing their influence. This is the same situation in the task of estimating human pose, and the appropriate example is that Vision Transformer-based ViTPose maintains the best performance in all human pose estimation benchmarks such as COCO, OCHuman, and MPII. However, because Vision Transformer has a heavy model structure with a large number of parameters and requires a relatively large amount of computation, it costs users a lot of money in learning. Therefore, this paper proposes a model that can perform human pose estimation tasks through a MobileViT-based model with fewer parameters and faster estimation. The proposed model is the Validation Set provided by the MS COCO human pose estimation benchmark, which showed 3.28GFLOPs and 9.72 million parameters of 1/5 and 1/9 compared to ViTPose, respectively, and showed relatively good performance by achieving 69.4 Mean Average Precision.


<img width="800" height="400" src="architecture.png"/>

## Results and Models
### Results on COCO val2017 on COCO val2017 dataset

| Model  | Backbone | #Params(M) | FLOPs(G) | Input Resolution | Feature Resolution | AP | AR |
| :----------------- | :-----------: | :------: | :-----------: | :------: |:------: | :------: | :------: | 
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

### Transfer Learning Result

| Model | Pretrain |AP | AP(50) | AP(75) | AR | AR(50) | AR(75) |
| :----------------- | :------: | :-----------: | :------: | :-----------: | :------: |:------: | :------: |
| MobileViTPose-XXS | None | 60.2 | 84.8 | 66.7 | 66.5 | 89.4 | 72.7 | 
| MobileViTPose-S | None | 63.9 | 86.2 | 70.8 | 69.9 | 1/4 | 90.4 | 76.3 | 
| MobileViTPose-XXS | ImageNet-1K | 61.7 | 86.1 | 69.0 | 67.9 | 90.5 | 74.6 | 
| MobileViTPose-S | ImageNet-1K | 69.4 | 88.8 | 77.0 | 74.9 | 1/4 | 92.8 | 82.0 | 


## Enviroment
NVIDIA Geforce RTX 3060

## Requirements

- Linux (Windows is not officially supported)
- Python 3.6+
- PyTorch 1.3+
- CUDA 9.2+ (If you build PyTorch from source, CUDA 9.0 is also compatible)
- GCC 5+
- [mmcv](https://github.com/open-mmlab/mmcv) (Please install the latest version of mmcv-full)
- Numpy
- cv2
- json_tricks
- [xtcocotools](https://github.com/jin-s13/xtcocoapi)

  ### Installation
<!-- The code is based on [MMPose](https://github.com/open-mmlab/mmpose).
You need clone the mmpose project and integrate the codes into mmpose first. -->

a. Install mmcv, we recommend you to install the pre-build mmcv as below.

```shell
pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/{cu_version}/{torch_version}/index.html
```

Please replace ``{cu_version}`` and ``{torch_version}`` in the url to your desired one. For example, to install the latest ``mmcv-full`` with ``CUDA 11`` and ``PyTorch 1.7.0``, use the following command:

```shell
pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu110/torch1.7.0/index.html
```

If it compiles during installation, then please check that the cuda version and pytorch version **exactly"" matches the version in the mmcv-full installation command. For example, pytorch 1.7.0 and 1.7.1 are treated differently.
See [here](https://github.com/open-mmlab/mmcv#installation) for different versions of MMCV compatible to different PyTorch and CUDA versions.

Optionally you can choose to compile mmcv from source by the following command

```shell
git clone https://github.com/open-mmlab/mmcv.git
cd mmcv
MMCV_WITH_OPS=1 pip install -e .  # package mmcv-full, which contains cuda ops, will be installed after this step
# OR pip install -e .  # package mmcv, which contains no cuda ops, will be installed after this step
cd ..
```

Or directly run

```shell
pip install mmcv-full
# alternative: pip install mmcv
```

**Important:** You need to run `pip uninstall mmcv` first if you have mmcv installed. If mmcv and mmcv-full are both installed, there will be `ModuleNotFoundError`.

b. Install build requirements

```shell
pip install -r requirements.txt
```

### Prepare datasets

It is recommended to symlink the dataset root to `$LITE_HRNET/data`.
If your folder structure is different, you may need to change the corresponding paths in config files.

**For COCO data**, please download from [COCO download](http://cocodataset.org/#download), 2017 Train/Val is needed for COCO keypoints training and validation. [HRNet-Human-Pose-Estimation](https://github.com/HRNet/HRNet-Human-Pose-Estimation) provides person detection result of COCO val2017 to reproduce our multi-person pose estimation results. 
Download and extract them under `$LITE_HRNET/data`, and make them look like this:

```
mobilevitpose
├── configs
├── models
├── tools
`── data
    │── coco
        │-- annotations
        │   │-- person_keypoints_train2017.json
        │   |-- person_keypoints_val2017.json
        |-- person_detection_results
        |   |-- COCO_val2017_detections_AP_H_56_person.json
        │-- train2017
        │   │-- 000000000009.jpg
        │   │-- 000000000025.jpg
        │   │-- 000000000030.jpg
        │   │-- ...
        `-- val2017
            │-- 000000000139.jpg
            │-- 000000000285.jpg
            │-- 000000000632.jpg
            │-- ...

```

## Training and Testing
All outputs (log files and checkpoints) will be saved to the working directory,
which is specified by `work_dir` in the config file.

By default we evaluate the model on the validation set after each epoch, you can change the evaluation interval by modifying the interval argument in the training config


### Training

```shell
# train with a signle GPU
python tools/train.py ${CONFIG_FILE} [optional arguments]

# train with multiple GPUs
./tools/dist_train.sh ${CONFIG_FILE} ${GPU_NUM} [optional arguments]
