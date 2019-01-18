# S3FD: Single Shot Scale-invariant Face Detector

[![Build Status](https://travis-ci.org/weiliu89/caffe.svg?branch=ssd)](https://travis-ci.org/weiliu89/caffe)
[![License](https://img.shields.io/badge/license-BSD-blue.svg)](LICENSE)



### Contents
1. [Installation](#installation)
2. [Preparation](#preparation)
3. [Train](#traineval)
4. [Eval](#models)
5. [Reference](#links)

### Installation
1. Get the code. We will call the directory that you cloned Caffe into `$CAFFE_ROOT`
  ```Shell
  # 1. realize scale-compensation anchor matching strategy
  # 2. realize random cropping square patches from original image 
  git clone git@github.com:lippman1125/caffe_s3fd.git
  cd caffe
  git checkout ssd
  ```


### Preparation
1. Download [fully convolutional reduced (atrous) VGGNet](https://gist.github.com/weiliu89/2ed6e13bfd5b57cf81d6). <br>
   By default, we assume the model is stored in `$CAFFE_ROOT/examples/s3fd/`


  ```

2. Create the LMDB file.
  ```Shell
  cd $CAFFE_ROOT
  # Create the trainval.txt, test.txt, and test_name_size.txt in data/FACE/
  ./data/FACE/create_list.sh
  # You can modify the parameters in create_data.sh if needed.
  # It will create lmdb files for trainval and test with encoded original image:
  #   - $HOME/data/faces_database/FACE/lmdb/FACE_trainval_lmdb
  #   - $HOME/data/faces_database/FACE/lmdb/FACE_test_lmdb
  # and make soft links at examples/VOC0712/
  ./data/FACE/create_data.sh
  ```

### Train
1. Train your model .
  ```
  ./build/tools/caffe train --solver examples/s3fd/solver.prototxt  --gpu 1 --weights examples/s3fd/VGG_ILSVRC_16_layers_fc_reduced.caffemodel
  ```
 
### Eval
1. ROC of FDDB compared with official, as follow:<br>
![data](https://github.com/lippman1125/github_images/blob/master/s3fd_images/roc.png)

2. ROC of FDDB compared with SSH/MTCNN, as follow:<br>
![data](https://github.com/lippman1125/github_images/blob/master/s3fd_images/roc_compares.png)

3. examples<br>
![data](https://github.com/lippman1125/github_images/blob/master/s3fd_images/example1.jpg)<br>
![data](https://github.com/lippman1125/github_images/blob/master/s3fd_images/example2.jpg)

### Reference
1. https://github.com/sfzhang15/SFD