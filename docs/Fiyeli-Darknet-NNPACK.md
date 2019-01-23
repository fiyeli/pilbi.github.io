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
sudo apt-get install ninja
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
ninja -j 1 # You can remove -j 1 to enable multithreading but it's dangerous on raspberry
sudo cp -a lib/* /usr/lib/
sudo cp include/nnpack.h /usr/include/
sudo cp deps/pthreadpool/include/pthreadpool.h /usr/include/
```
Build darknet-nnpack
```
git clone https://github.com/fiyeli/Fiyeli-Darknet-NNPACK
cd darknet-nnpack
make
```

## Weights
We recommand using the yolov3 weights released by darknet. You can download it using : 
```
wget https://pjreddie.com/media/files/yolov2.weights
```
Other weight files can be downloaded from the [YOLO homepage](https://pjreddie.com/darknet/yolo/).

## Run person detection
The main executable returns the number of persons detected on the picture when used with the "person" mode.
```console
YOLOv2
./darknet detector person cfg/coco.data cfg/yolov2.cfg yolov2.weights data/person.jpg
```
