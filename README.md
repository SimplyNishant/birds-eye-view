# birds-eye-view

Welcome to the code repository for obtaining the bird's eye view of a scene from a single input image. The code estimates the homography matrix for a bird's eye view transformation along with some of the cameras's intrinsic and extrinsic parameters.

## Pre-requisites

This code was written in TensorFlow 1.8 and Python 3.6.8 (unless specified otherwise). However, it has been tested until TensorFlow 1.13.1 and may work with other Python versions as well.
Some of the main libraries being used are:

1. TensorFlow
2. OpenCV
3. Numpy
4. Matplotlib (for visualization)

### Creating virtual env

If you want to create a fresh environment, you can install the pre-requisite packages by running the following command in the main code directory:

```
pip install -r requirements.txt
```

**Note:** You will need to install TensorFlow separately. I have removed tensorflow from requirements because it depends on CUDA version etc.

## How to run?

### Generate CARLA-VP dataset

This script specifically requires Python 3.7.* if you intend to use it without any modification. This is because it was written for CARLA 0.9.4 in Windows 10 experimental version. To run, first start CARLA engine, then open the terminal and type:

```
python scripts/generate_carla_van_dataset.py
```

**Note**: The parameters can be changed in the file (lines 202-232 currently) directly.

### Training on CARLA-VP dataset

Open the terminal and type:

```
python scripts/train_carla_van_horizon_vpz.py \
  --dataset_dir=<train-CARLA-VP.tfrecords \
  --train_dir=<experiment_dir> \
  --checkpoint_path=<vgg_16.ckpt> \
  --checkpoint_exclude_scopes=vgg_16/fc8 \
  --model_name=vgg-16 \
  --save_summaries_secs=30 \
  --save_interval_secs=300 \
  --learning_rate=0.001 \
  --optimizer=adam \
  --batch_size=16
```

### Predicting bird's eye view from a single image

Open the terminal and type:

```
python scripts/predict_7kcarla_horizon_vpz_homography.py 
    --img_path $IMAGE_PATH 
    --model_name $CNN_MODEL
```

where:

__$IMAGE_PATH:__ path to the image

__$CNN_MODEL:__ name of the cnn model you want to use (available options: vgg-16, inception-v4) 
