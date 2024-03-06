# TensorRT安装

## 获取TensorRT压缩包

- 在[官网](https://developer.nvidia.com/nvidia-tensorrt-8x-download)下载`TensorRT-8.6.0.12.Linux.x86_64-gnu.cuda-11.8.tar.gz`
- 解压

```shell
tar -zxvf TensorRT-8.6.0.12.Linux.x86_64-gnu.cuda-11.8.tar.gz
```
- 添加环境变量

```shell
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:xxx/TensorRT-8.6.0.12/lib
```

- 安装

```shell
cd TensorRT-8.6.0.12/python/
python3 -m pip install tensorrt-8.6.0-cp37-none-linux_x86_64.whl
```

- 推理示例

[TensorRT sample YOLOV3](https://github.com/NVIDIA/TensorRT/blob/release/8.6/samples/python/yolov3_onnx/onnx_to_tensorrt.py)