# Installation
# Darknet with NNPACK
NNPACK was used to optimize [Darknet](https://github.com/pjreddie/darknet) without using a GPU. It is useful for embedded devices using ARM CPUs.

## Build from Raspberry Pi 3
Log in to Raspberry Pi using SSH.<br/>
Install [PeachPy](https://github.com/Maratyszcza/PeachPy) and [confu](https://github.com/Maratyszcza/confu)
```
sudo pip install --upgrade git+https://github.com/Maratyszcza/PeachPy
sudo pip install --upgrade git+https://github.com/Maratyszcza/confu
```
Install [Ninja](https://ninja-build.org/)
```
git clone https://github.com/ninja-build/ninja.git
cd ninja
git checkout release
./configure.py --bootstrap
export NINJA_PATH=$PWD
```
Install clang
```
sudo apt-get install clang
```
Install [NNPACK-darknet](https://github.com/digitalbrain79/NNPACK-darknet.git)
```
git clone https://github.com/digitalbrain79/NNPACK-darknet.git
cd NNPACK-darknet
confu setup
python ./configure.py --backend auto
$NINJA_PATH/ninja
sudo cp -a lib/* /usr/lib/
sudo cp include/nnpack.h /usr/include/
sudo cp deps/pthreadpool/include/pthreadpool.h /usr/include/
```
Build darknet-nnpack
```
git clone https://github.com/digitalbrain79/darknet-nnpack.git
cd darknet-nnpack
make
```

## Weights
We recommand using the yolov3 weights released by darknet. You can download it using : 
```
wget https://pjreddie.com/media/files/yolov3.weights
```
Other weight files can be downloaded from the [YOLO homepage](https://pjreddie.com/darknet/yolo/).

## Run person detection
The main executable returns the number of persons detected on the picture when used with the "person" mode.
```console
YOLOv3
./darknet detector person cfg/coco.data cfg/yolov3.cfg yolov3.weights data/person.jpg
```

## Result
Model | Build Options | Prediction Time (seconds)
:-:|:-:|:-:
YOLOv2-tiny | NNPACK=1,ARM_NEON=1 | 1.8
YOLOv2-tiny | NNPACK=0,ARM_NEON=0 | 31
YOLOv3-tiny | NNPACK=1,ARM_NEON=1 | 2.0
YOLOv3-tiny | NNPACK=0,ARM_NEON=0 | 32
