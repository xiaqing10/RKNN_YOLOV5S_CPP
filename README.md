# Yolo-v5 demo
This Demo shows yolo-v5 RKNN model object detection. We refer to repository:https://github.com/airockchip/yolov5. 

步骤：
  参考上述链接训练，里面的yolov5和官方的大致修改了两个部分，一个是focus层，直接用卷积替代，一个是silu->relu，增加速度。
  然后转Onnx -> rknn，这个都是工程里面带的，测试了很多遍，无坑。
  
  然后编译本工程，本工程基于rk3300pro测试，里面有个测试模型，三分类，opencv库，rknn库，和drm库，可以直接编译运行。若用自己的模型，修改类别即可。
