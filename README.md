# Welcome to the OpenCV Tensorflow C++ Example for XCode!


## Example Run & Output

```
$ ./OpenCVTensorflowExample example-input.jpg
Loaded 183 dnn class labels
Inference time, ms: 1284.07
Total detections before threshold: 100
Detection 1: class: 1 person, confidence: 90.2028%, box: (121.05,163.801), (134.757,196.974)
Detection 2: class: 1 person, confidence: 87.3808%, box: (52.6214,169.068), (63.0605,188.564)
Detection 3: class: 1 person, confidence: 84.4214%, box: (215.297,166.339), (226.054,197.066)
Detection 4: class: 1 person, confidence: 83.5167%, box: (237.044,167.841), (246.486,193.557)
Detection 5: class: 1 person, confidence: 66.0681%, box: (355.306,164.001), (369.623,206.001)
Detection 6: class: 1 person, confidence: 62.8306%, box: (26.3063,152.234), (33.2975,171.126)
Detection 7: class: 1 person, confidence: 62.6159%, box: (351.111,167.912), (360.04,193.69)
Detection 8: class: 38 kite, confidence: 61.8607%, box: (73.5419,62.0797), (94.6284,75.9994)
Detection 9: class: 1 person, confidence: 56.8792%, box: (190.821,163.331), (195.611,178.345)
Detection 10: class: 1 person, confidence: 54.8295%, box: (285.021,182.843), (316.235,252.078)
Detection 11: class: 1 person, confidence: 54.7891%, box: (193.142,166.008), (199.851,183.763)
Total detections: 11
```

A cv window will also popup with the image and boxes drawn around it, and will also be saved to a constant file path that you specify.

## Setup & Installation

I wish this was easier, but alas, you'll have to do all of this.

### Download Tensorflow model & labels file

First, find a COCO model at https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md and download it.

Fix line by replacing the value of `TF_PB_PATH` with your local path
```
std::string TF_PB_PATH = "/PATH/TO/COCO/frozen_inference_graph.pb";
```

Second, find the labels file at https://github.com/ActiveState/gococo/blob/master/labels.txt

Fix line by replacing the value of `TF_LABELLIST_PATH` with your local path
```
std::string TF_LABELLIST_PATH = "/PATH/TO/COCO/labels.txt";
```

### Set Input and Output Image PATH
Fix the two lines of where you'll have your images, by replacing the values of `DEFAULT_IMAGE_PATH` and `OUTPUT_IMAGE_PATH` with your own values
```
cv::String DEFAULT_IMAGE_PATH = "/PATH/TO/IMAGES/input.jpg";
cv::String OUTPUT_IMAGE_PATH = "/PATH/TO/IMAGES/output.jpg";
```

### Build Tensorflow

* Download Tensorflow https://github.com/tensorflow/tensorflow/tags
* Run `./configure` and `bazel build` (you'll have to get bazel with `brew install bazel`)
* _Also_ run `bazel build //tensorflow:libtensorflow.so`
* `brew install protobuf 3.4.1`
* Download nsync master @ https://github.com/google/nsync
* Download eigen devel @ http://bitbucket.org/eigen/eigen/get/default.zip

### Install OpenCV

* Make sure you install OpenCV, which is easiest by `brew install opencv` or `brew upgrade opencv`


## Linking Before Compilation

### Linker flags

Add the following to your *Other Linker Flags*

* -lopencv_core
* -lopencv_imgproc
* -lopencv_imgcodecs
* -lopencv_shape
* -lopencv_highgui
* -ltensorflow_framework
* `-force_load /PATH/TO/bazel-out/.../libtensorflow.so`

Example:

![Linker Flags](https://github.com/moorage/OpenCVTensorflowExample/raw/master/readme-linker-flags.png "Linker Flags")


### Header Search Paths

Add the following to your *Header Search Paths*

* /PATH/TO/nsync/public
* /PATH/TO/opencv/include
* /PATH/TO/protobuf/include
* /PATH/TO/eigen-devel
* /PATH/TO/tensorflow/bazel-devel
* /PATH/TO/tensorflow/

Example:

![Header Search Paths](https://github.com/moorage/OpenCVTensorflowExample/raw/master/readme-header-search-paths.png "Header Search Paths")



### Library Search Paths

Add the following to your *Library Search Paths*

* /PATH/TO/opencv/lib
* /PATH/TO/tensorflow/bazel-bin/tensorflow

Example:

![Library Search Paths](https://github.com/moorage/OpenCVTensorflowExample/raw/master/readme-library-search-paths.png "Library Search Paths")
