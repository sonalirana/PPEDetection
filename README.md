# PPE App
Work Place hazards are something which you can’t avoid, especially in occupations such as construction, mining or chemical laboratories. Yet from an organizational perspective, you can try your best to minimize them through the use of Personal Protective equipment.The importance of PPE cannot be stressed enough, with on-site fatalities on a greater rise leading to a rise in compensation and additional expenditure. Organizations need to promote the use of PPE amongst the very DNA of their work culture. This app, built on Nvidia's Deepsteam SDK, would help identify the helmet and gloves as a part of PPE which is mandatory and life saving during various industry operations. 

![PPE](misc/ppe.png)

## Citations

* [ultralytics](https://github.com/ultralytics/yolov5)
* [aj-ames/Hermes-Deepstream](https://github.com/aj-ames/Hermes-Deepstream.git)

## Index

1. [Introduction](#Introduction)
2. [Deepstream Setup](#Deepstream-Setup)
    1. [Install System Dependencies](#Install-System-Dependencies)
    2. [Install Deepstream](#Install-Deepstream)
3. [Running the Application](#Running-the-Application)
    1. [Clone the repository](#Cloning-the-repository)
    2. [Run with different input sources](#Run-with-different-input-sources)

## Introduction

The PPE Detection Application consists of a pipleline powered by Deepstream, that can be run on Nvidia power DGPU's as well as Jetson Devices such as the Jetson Xavier NX, Jeson Nano, Jetson Xavier AGX and the TX2.

![Jetson](misc/jetson.jpg)

## Deepstream Setup

This post assumes you have a fully functional Jetson device. If not, you can refer the documentation [here](https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html).

### 1. Install System Dependencies

```sh
sudo apt install \
libssl1.0.0 \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstrtspserver-1.0-0 \
libjansson4=2.11-1
uuid \
uuid-dev
```

### 2. Install Deepstream on Dgpu's

Download the DeepStream 5.1 Debian package `deepstream-5.1_5.1.0-1_amd64.deb`, to the DGPU device from [here](https://developer.nvidia.com/deepstream-sdk-download-tesla-archived). Then enter the command:

```sh
sudo apt-get install ./deepstream-5.1_5.1.0-1_amd64.deb
```

### 3. Install Deepstream in Jetson Devices

Download the deb file under - DeepStream 5.1 for Jetson from [here](https://developer.nvidia.com/embedded/deepstream-on-jetson-downloads-archived).

```sh
sudo apt-get install ./deepstream-5.1_5.1.0-1_amd64.deb
```

## Run the Application

### 1. Clone the repository

First, install git and git-lfs

```sh
sudo apt install git git-lfs
```

Next, clone the repository

```sh
# Using HTTPS
git clone https://github.com/sonalirana/PPE.git
# Using SSH
git clone git@github.com:sonalirana/PPE.git
```

Now, enable lfs and pull the yolo weights

```sh
git lfs install
git lfs pull
```

### 2. Run with different input sources

The computer vision part of the solution can be run on one or many input sources of multiple types, all powered using NVIDIA Deepstream.

Firstly, we must build the application by running the following command:

```sh
make clean && make -j$(nproc)
```

This will generate the binary called `ppe-app`. This is a one-time step and you need to do this only when you make source-code changes.

Next, create a file called `inputsources.txt` and paste the path of videos or rtsp url of CCTV IP cameras.

```sh
file:///home/raman/Downloads/ppe2.mp4
```

Now, run the application by running the following command:

```sh
./ppe-app
```

Please find the Links to a couple of Demo videos, [here](https://youtu.be/tBgqcJZn1O0)

and [here](https://youtu.be/c6zSTo0pGFQ)
