# Welcome to the OpenCV Tensorflow C++ Example for XCode!


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
