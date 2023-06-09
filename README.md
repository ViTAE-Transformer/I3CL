<h1 align="center">I3CL: Intra- and Inter-Instance Collaborative Learning for Arbitrary-shaped Scene Text Detection</h1> 

<p align="center">
<a href="https://arxiv.org/abs/2108.01343v3"><img src="https://img.shields.io/badge/arXiv-Paper-<color>"></a> <a href="https://link.springer.com/article/10.1007/s11263-022-01616-6"><img src="https://img.shields.io/badge/publication-Paper-<color>"></a>
</p>

<p align="center">
  <a href="#updates">Updates</a> |
  <a href="#introduction">Introduction</a> |
  <a href="#results">Results</a> |
  <a href="#usage">Usage</a> |
  <a href="#citation">Citation</a> |
  <a href="#acknowledgment">Acknowledgment</a>
</p >
This is the repo for [IJCV'22] "I3CL: Intra- and Inter-Instance Collaborative Learning for Arbitrary-shaped Scene Text Detection". I3CL with ViTAEv2, ResNet50 and ResNet50 w/ RegionCL backbone are included.

***

## Updates
>***[2022/04/13]*** Publish links of training datasets.
>
>***[2022/04/11]*** Add SSL training code for this implementation.
>
>***[2022/04/09]*** The training code for ICDAR2019 ArT dataset is uploaded.
>
>***[2021/07/05]*** Ranks the first at [ICDAR2019 ArT leaderboard](https://rrc.cvc.uab.es/?ch=14&com=evaluation&task=1).
>
> Other applications of ViTAE Transformer: [**Image Classification**](https://github.com/ViTAE-Transformer/ViTAE-Transformer/tree/main/Image-Classification) | [**Object Detection**](https://github.com/ViTAE-Transformer/ViTAE-Transformer/tree/main/Object-Detection) | [**Sementic Segmentation**](https://github.com/ViTAE-Transformer/ViTAE-Transformer/tree/main/Semantic-Segmentation) | [**Animal Pose Estimation**](https://github.com/ViTAE-Transformer/ViTAE-Transformer/tree/main/Animal-Pose-Estimation) | [**Matting**](https://github.com/ViTAE-Transformer/ViTAE-Transformer-Matting) | [**Remote Sensing**](https://github.com/ViTAE-Transformer/ViTAE-Transformer-Remote-Sensing)

## Introduction

Existing methods for arbitrary-shaped text detection in natural scenes face two critical issues, i.e., 1) fracture detections at the gaps in a text instance; and 2) inaccurate detections of arbitrary-shaped text instances with diverse background context. To address these issues, we propose a novel method named Intra- and Inter-Instance Collaborative Learning (I3CL). Specifically, to address the first issue, we design an effective convolutional module with multiple receptive fields, which is able to collaboratively learn better character and gap feature representations at local and long ranges inside a text instance. To address 
the second issue, we devise an instance-based transformer module to exploit the dependencies between different text instances and a global context module to exploit the semantic context from the shared background, which are able to collaboratively learn more discriminative text feature representation. In this way, I3CL can effectively exploit the intra- and inter-instance dependencies together in a unified end-to-end trainable framework. Besides, to make full use of the unlabeled data, we design an effective semi-supervised learning method to leverage the pseudo labels via an ensemble strategy. Without bells and whistles, experimental results show that the proposed I3CL sets new state-of-the-art results on three challenging public benchmarks, i.e., an F-measure of 77.5% on ArT, 86.9% on Total-Text, and 86.4% on CTW-1500. Notably, our I3CL with the ResNeSt-101 backbone ranked the 1st place on the ArT leaderboard.

![image](./I3CL.jpg)

## Results

Example results from paper.

![image](./demo.jpg)

Evaluation results of I3CL with different backbones on ArT. *Note that: (1) I3CL with ViTAE only adopts one training stage with LSVT+MLT19+ArT training datasets in this repo. ResNet series adopt three training stages, i.e, pre-train on SynthText, mix-train on ReCTS+RCTW+LSVT+MLT19+ArT and lastly finetune on LSVT+MLT19+ArT. (2) Original implementation of ResNet series is based on Detectron2. The results and model links of ResNet-50 will be updated soon in this implementation.*

|Backbone|Model Link|Training Data|Recall|Precision|F-measure|
|:------:|:------:|:------:|:------:|:------:|:------:|
|<p>ViTAEv2-S<br>[**this repo**]</p>|<p>[OneDrive](https://1drv.ms/u/s!AimBgYV7JjTlgRH63hbJjWub5VMv?e=XUOrLb)/<br>[百度网盘](https://pan.baidu.com/s/1UQ8WUlk5dtRRJIKgZTWBXA) (pw:w754)</p>|LSVT,MLT19,ArT|**75.4**|82.8|78.9|
|<p>ResNet-50<br>[paper]</p>|-|<p>SynthText800K<br>ReCTS,RCTW,LSVT,MLT19,ArT</p>|71.3|82.7|76.6|
|<p>ResNet-50<br>[**this repo**]</p>|<p>[OneDrive](https://1drv.ms/u/s!AimBgYV7JjTlgRzYxRbnM2IBfbXR?e=2QNzq6)/<br>[百度网盘](https://pan.baidu.com/s/1uhk3nQi48yxgT-W82xtgSw) (pw:acy0)</p>|<p>SynthText150K<br>ReCTS,RCTW,LSVT,MLT19,ArT</p>|73.7|81.2|77.3|
|<p>ResNet-50 w/ RegionCL(finetuning)<br>[paper]</p>|-|<p>SynthText800K<br>ReCTS,RCTW,LSVT,MLT19,ArT</p>|72.6|81.9|77.0|
|<p>ResNet-50 w/ RegionCL(finetuning)<br>[**this repo**]</p>|<p>[OneDrive](https://1drv.ms/u/s!AimBgYV7JjTlgR0EnuXCFbYD-SVG?e=fXaEfa)/<br>[百度网盘](https://pan.baidu.com/s/1bXgJpEn5kX1sWmZoukddjg) (pw:k13v)</p>|<p>SynthText150K<br>ReCTS,RCTW,LSVT,MLT19,ArT</p>|75.4|80.6|77.9|
|<p>ResNet-50 w/ RegionCL(w/o finetuning)<br>[paper]</p>|-|<p>SynthText800K<br>ReCTS,RCTW,LSVT,MLT19,ArT</p>|73.5|81.6|77.3|
|<p>ResNet-50 w/ RegionCL(w/o finetuning)<br>[**this repo**]</p>|<p>[OneDrive](https://1drv.ms/u/s!AimBgYV7JjTlgSCIBmXyBVoMpj-S?e=ajfdio)/<br>[百度网盘](https://pan.baidu.com/s/1B84UAfV3S5R6HzBR8j_P6w) (pw:7k84)</p>|<p>SynthText150K<br>ReCTS,RCTW,LSVT,MLT19,ArT</p>|75.1|80.6|77.8|

## Usage

### Install

>**Prerequisites：**
>
>- Linux (macOS and Windows are not tested)
>- Python >= 3.6
>- Pytorch >= 1.8.1 (For ViTAE implementation). Please make sure your compilation CUDA version and runtime CUDA version match.
>- GCC >= 5
>- MMCV (We use mmcv-full==1.4.3)

1. Create a conda virtual environment and activate it. Note that this implementation is based on mmdetection 2.20.0 version.

2. Install Pytorch and torchvision following [official instructions](https://pytorch.org).

3. Install mmcv-full and timm. Please refer to [mmcv](https://github.com/open-mmlab/mmcv) to install the proper version. For example:
   
    ```
    pip install mmcv-full==1.4.3 -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.9.0/index.html
    pip install timm
    ```

4. Clone this repository and then install it:
   
    ```
    git clone https://github.com/ViTAE-Transformer/ViTAE-Transformer-Scene-Text-Detection.git
    cd ViTAE-Transformer-Scene-Text-Detection
    pip install -r requirements/build.txt
    pip install -r requirements/runtime.txt
    pip install -v -e .
    ```

### Preparation

**Model:** 

- To train I3CL model yourself, please download the pretrained ViTAEv2 used in this implementation from here: [OneDrive](https://1drv.ms/u/s!AimBgYV7JjTlgRKwMDLQQ7QzPOJs?e=mzeeO4) | [百度网盘](https://pan.baidu.com/s/1su-IP6Gl1VJKBHfwtKIoow) (pw:petb). ResNet-50 w/ RegionCL(finetuning): [OneDrive](https://1drv.ms/u/s!AimBgYV7JjTlgRNs8EMQlB1SI6CO?e=KaSQtl) | [百度网盘](https://pan.baidu.com/s/1T2vmyQOpjzIfPveKKwZr-Q) (pw:y598). ResNet-50 w/ RegionCL(w/o finetuning): [OneDrive](https://1drv.ms/u/s!AimBgYV7JjTlgRTlX8j-HfnHNG6c?e=bixznC) | [百度网盘](https://pan.baidu.com/s/1_6nVTdxRpUi5kwp1MhTI9g) (pw:cybh). For backbone initialization, please put them in [pretrained_model/ViTAE](./pretrained_model/ViTAE) or [pretrained_model/RegionCL](./pretrained_model/RegionCL).
- Full I3CL model with ViTAE backbone trained on ArT can be downloaded and put in [pretrained_model/I3CL](./pretrained_model/I3CL).

**Data**

- Coco format training datasets are utilized. Some offline augmented ArT training datasets are used. `lsvt-test` is only used to train SSL(**S**emi-**S**upervised **L**earning) model in paper. Files named `train_lossweight.json` are the provided pseudo-label for SSL training. You can download correspoding datasets in config file from here and put them in [data/](./data):

    |Dataset|<p>Link<br>(OneDrive)</p>|<p>Link<br>(Baidu Wangpan百度网盘)</p>|
    |:------:|:------:|:------:|
    |art|[Link](https://1drv.ms/u/s!AimBgYV7JjTlgTxZ8iqLlXrv90Nj?e=XeMELU)|[Link](https://pan.baidu.com/s/1Iit8TXZCOW76ND7NknjemQ) (pw:lvja)|
    |art_light|[Link](https://1drv.ms/u/s!AimBgYV7JjTlae-oSHbbwqD-H8o?e=KJUhgt)|[Link](https://pan.baidu.com/s/1u_O4AywAu_FBfkpjJN2IFQ) (pw:mzrk)|
    |art_noise|[Link](https://1drv.ms/u/s!AimBgYV7JjTlgT0RMMfGVTzioT-C?e=wiGD3q)|[Link](https://pan.baidu.com/s/1ErIrOMoSNbaoEBCQSCGY7Q) (pw:m71o)|
    |art_sig|[Link](https://1drv.ms/u/s!AimBgYV7JjTlbdAx1ZOCpvmYkBE?e=NNxguj)|[Link](https://pan.baidu.com/s/1bSJ321LNl7IISXra24f6eA) (pw:cdk8)|
    |lsvt|[Link](https://1drv.ms/u/s!AimBgYV7JjTlae-oSHbbwqD-H8o?e=EjB9d5)|[Link](https://pan.baidu.com/s/1UTdD8fcdyXXdQMzfMBbHoQ) (pw:wly0)|
    |lsvt_test|[Link](https://1drv.ms/u/s!AimBgYV7JjTldfOea-7Wcc_uVSE?e=I1IgvU)|[Link](https://pan.baidu.com/s/14y3W0XRCuqDboSXMlXTtJw) (pw:8ha3)|
    |icdar2019_mlt|[Link](https://1drv.ms/u/s!AimBgYV7JjTlbtKKo7-IFG32Yo4?e=XprWJb)|[Link](https://pan.baidu.com/s/1vHN6i4iTtUsDMa6eR7Py0Q) (pw:hmnj)|
    |rctw|[Link](https://1drv.ms/u/s!AimBgYV7JjTlgRawI3dSiEOhp6Is?e=D7MktG)|[Link](https://pan.baidu.com/s/1b6_pV1McdntgtudjdtVTLA) (pw:ngge)|
    |rects|[Link](https://1drv.ms/u/s!AimBgYV7JjTlgRWNyPwC5a04c-vX?e=hKK4az)|[Link](https://pan.baidu.com/s/1wp1Qrm28Ycr4s-Asl4-x6Q) (pw:y00o)|

    The file structure should look like:
    ```
    |- data
        |- art
        |   |- train_images
        |   |    |- *.jpg
        |   |- test_images
        |   |    |- *.jpg
        |   |- train.json
        |   |- train_lossweight.json
        |- art_light
        |   |- train_images
        |   |    |- *.jpg
        |   |- train.json
        |   |- train_lossweight.json
        ......
        |- lsvt
        |   |- train_images1
        |   |    |- *.jpg
        |   |- train_images2
        |   |    |- *.jpg
        |   |- train1.json
        |   |- train1_lossweight.json
        |   |- train2.json
        |   |- train2_lossweight.json
        |- lsvt_test
        |   |- train_images
        |   |    |- *.jpg
        |   |- train_lossweight.json
        ......

### Training

- Distributed training with 4GPUs for **ViTAE** backbone:
```
python -m torch.distributed.launch --nproc_per_node=4 --master_port=29500 tools/train.py \
configs/i3cl_vitae_fpn/i3cl_vitae_fpn_ms_train.py --launcher pytorch --work-dir ./out_dir/${your_dir}
```

- Distributed training with 4GPUs for **ResNet50** backbone:


`stage1`:
```
python -m torch.distributed.launch --nproc_per_node=4 --master_port=29500 tools/train.py \
configs/i3cl_r50_fpn/i3cl_r50_fpn_ms_pretrain.py --launcher pytorch --work-dir ./out_dir/art_r50_pretrain/
```
`stage2`:
```
python -m torch.distributed.launch --nproc_per_node=4 --master_port=29500 tools/train.py \
configs/i3cl_r50_fpn/i3cl_r50_fpn_ms_mixtrain.py --launcher pytorch --work-dir ./out_dir/art_r50_mixtrain/
```
`stage3`:
```
python -m torch.distributed.launch --nproc_per_node=4 --master_port=29500 tools/train.py \
configs/i3cl_r50_fpn/i3cl_r50_fpn_ms_finetune.py --launcher pytorch --work-dir ./out_dir/art_r50_finetune/
```

- Distributed training with 4GPUs for **ResNet50 w/ RegionCL** backbone:

`stage1`:
```
python -m torch.distributed.launch --nproc_per_node=4 --master_port=29500 tools/train.py \
configs/i3cl_r50_regioncl_fpn/i3cl_r50_fpn_ms_pretrain.py --launcher pytorch --work-dir ./out_dir/art_r50_regioncl_pretrain/
```
`stage2`:
```
python -m torch.distributed.launch --nproc_per_node=4 --master_port=29500 tools/train.py \
configs/i3cl_r50_regioncl_fpn/i3cl_r50_fpn_ms_mixtrain.py --launcher pytorch --work-dir ./out_dir/art_r50_regioncl_mixtrain/
```
`stage3`:
```
python -m torch.distributed.launch --nproc_per_node=4 --master_port=29500 tools/train.py \
configs/i3cl_r50_regioncl_fpn/i3cl_r50_fpn_ms_finetune.py --launcher pytorch --work-dir ./out_dir/art_r50_regioncl_finetune/
```

*Note:*

- *If the GPU memory is limited during training I3CL ViTAE backbone, please adjust `img_scale` in 
[configuration file](./configs/i3cl_vitae_fpn/coco_instance.py). The maximum scale set to (800, 1333) is proper for V100(16G) while 
there is little effect on the performance actually. Please change the training scale according to your condition.*

### Inference

For example, use our trained I3CL model to get inference results on ICDAR2019 ArT test set with visualization images, 
txt format records and the json file for testing submission, please run:

```
python demo/art_demo.py --checkpoint pretrained_model/I3CL/vitae_epoch_12.pth --score-thr 0.45 --json_file art_submission.json
```

*Note:*
 - Upload the saved json file to [ICDAR2019-ArT evaluation website](https://rrc.cvc.uab.es/?ch=14) for Recall, Precision and F1 evaluation results. 
 Change the path for saving visualizations and txt files if needed.

## Citation

This project is for research purpose only.

If you find I3CL useful in your research, please consider citing:
```
@article{du2022i3cl,
  title={I3CL: Intra-and Inter-Instance Collaborative Learning for Arbitrary-shaped Scene Text Detection},
  author={Du, Bo and Ye, Jian and Zhang, Jing and Liu, Juhua and Tao, Dacheng},
  journal={International Journal of Computer Vision},
  volume={130},
  number={8},
  pages={1961--1977},
  year={2022},
  publisher={Springer}
}
```

## Acknowledgement

Thanks for [mmdetection](https://github.com/open-mmlab/mmdetection).
