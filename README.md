## Training

**Follow the link below to see how the model was trained using Colab.**

<a href="https://colab.research.google.com/drive/1W2HhV12lEjV-dnm3gdujsjvSYQwTm4cB?usp=sharing"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a>

## Nuts & Bolts Detection

**How to use:**

*1. Clone the required repositories, install required packages and download pretrained weights:*

```bash
!git clone https://github.com/ultralytics/yolov5
!wget https://github.com/Stroma-Vision/machine-learning-challenge/releases/download/v0.1/challenge.zip
!unzip challenge.zip
!rm challenge.zip

%cd yolov5
!pip install -r requirements.txt
!pip install -r requirements.txt coremltools onnx onnx-simplifier onnxruntime openvino-dev tensorflow-cpu nvidia-tensorrt
!pip install onnxruntime-gpu
!wget https://github.com/sarpalgan/nuts-bolts/releases/download/v1.0.0/weights.zip
!unzip weights.zip
!rm weights.zip

%cd data
!wget https://github.com/sarpalgan/nuts-bolts/releases/download/v1.0.0/custom.yaml

%cd ..
```

*2. Run the following code to export best.py PyTorch model to ONNX and TensorRT formats:*

```bash
!python export.py --device 0 --weights best.pt --include engine --data data/data.yaml --conf-thres 0.1
```

*3. Make detection with one of the following code:*

- *replace:* `path/to/detection/file` *with*  `/content/challenge/images/test/test.mp4` *to make detection on test.mp4 file* 

```bash
# Detect with PyTorch
!python detect.py --name pt --weights best.pt --source path/to/detection/file --data data/custom.yaml  

# Detect with ONNX
!python detect.py --name onnx --weights best.onnx --source path/to/detection/file --data data/custom.yaml  

#Detect with TensorRT
!python detect.py --name engine --weights best.engine --source path/to/detection/file --data data/custom.yaml    
```

*4. Results will be saved into `runs/detect/model.extension`* 

`model.extension`
- `pt`   *(PyTorch)*
- `onnx`   *(ONNX)*
- `engine`   *(TensorRT)*
