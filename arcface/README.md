# arcface

The mxnet implementation is from [deepinsight/insightface.](https://github.com/deepinsight/insightface)

The pretrained model is [LResNet50E-IR,ArcFace@ms1m-refine-v1.](https://github.com/deepinsight/insightface/wiki/Model-Zoo#32-lresnet50e-irarcfacems1m-refine-v1)

The two images used in this project are joey0.ppm and joey1.ppm, download them from [Google Drive.](https://drive.google.com/drive/folders/1ctqpkRCRKyBZRCNwo9Uq4eUoMRLtFq1e)

<p align="center">
<img src="https://user-images.githubusercontent.com/15235574/83122953-f45f8d80-a106-11ea-84b0-4f6ff91b5924.jpg">
</p>

## Run

```
1. generate arcface-r50.wts from mxnet implementation with LResNet50E-IR,ArcFace@ms1m-refine-v1 pretrained model

git clone https://github.com/deepinsight/insightface
cd insightface/deploy
// copy tensorrtx/arcface/gen_wts.py to here(insightface/deploy)
// download model-r50-am-lfw.zip and unzip here(insightface/deploy)
python gen_wts.py
// a file 'arcface-r50.wts' will be generated.
// the master branch of insightface should work, if not, you can checkout 94ad870abb3203d6f31b049b70dd080dc8f33fca

2. put arcface-r50.wts into tensorrtx/arcface, build and run

cd tensorrtx/arcface
// download joey0.ppm and joey1.ppm, and put here(tensorrtx/arcface)
mkdir build
cd build
cmake ..
make
sudo ./arcface-r50 -s    // serialize model to plan file i.e. 'arcface-r50.engine'
sudo ./arcface-r50 -d    // deserialize plan file and run inference

3. check the output log, latency and similarity score.
```

## Config

- FP16/FP32 can be selected by the macro `USE_FP16` in arcface-r50.cpp
- GPU id can be selected by the macro `DEVICE` in arcface-r50.cpp

## More Information

See the readme in [home page.](https://github.com/wang-xinyu/tensorrtx)