## Introduction

A LibTorch inference implementation of the [yolov5](https://github.com/ultralytics/yolov5) object detection algorithm. Both GPU and CPU are supported.



## Dependencies

- Ubuntu 16.04
- CUDA 10.2
- OpenCV 4.1.0
- LibTorch 1.5.1



## TorchScript Model Export

Please refer to the official document here: https://github.com/ultralytics/yolov5/issues/251

Note that the current export script in [yolov5](https://github.com/ultralytics/yolov5) uses CPU by default,  the "export.py" needs to be modified as following to support GPU (can be found in "utils/export.py"):

```python
# line 22
img = torch.zeros((opt.batch_size, 3, *opt.img_size)).to(device='cuda')  
# line 26
model = torch.load(opt.weights, map_location=torch.device('cuda'))['model'].float()
# line 28
model.model[-1].export = False  
```



## Setup

```bash
$ cd /path/to/libtorch-yolo5
$ wget https://download.pytorch.org/libtorch/cu102/libtorch-cxx11-abi-shared-with-deps-1.5.1.zip
$ unzip libtorch-cxx11-abi-shared-with-deps-1.5.1.zip
$ mkdir build && cd build
$ cmake .. && make
$ ./libtorch-yolov5 <path-to-exported-script-module> <path-to-image> <-gpu>
```



To run inference on examples in the `./images` folder:

```bash
# CPU
$ ./libtorch-yolov5 ../weights/yolov5s.torchscript.pt ../images/bus.jpg
# GPU
$ ./libtorch-yolov5 ../weights/yolov5s_gpu.torchscript.pt ../images/bus.jpg -gpu
```



## Demo

![Bus](images/bus_out.jpg)



![Zidane](images/zidane_out.jpg)



## References

1. https://github.com/ultralytics/yolov5
2. https://github.com/walktree/libtorch-yolov3
3. https://pytorch.org/cppdocs/index.html
4. https://github.com/pytorch/vision

