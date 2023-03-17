# PS4 camera: The cheap high resolution 3D stereo camera for OpenCV and Python!

![](https://github.com/sieuwe1/PS4-eye-camera-for-linux-with-python-and-OpenCV/blob/main/demo.gif)

[![Demo](https://img.youtube.com/vi/c7CF6eDC0_A/0.jpg)](https://www.youtube.com/watch?v=c7CF6eDC0_A)

## Contents 

### 1: Intro
### 2: Installation
### 3: Changing Video Settings
### 4: Camera specifications
### 5: References 

## 1: Intro
Since the launch of the Xbox Kinect, a lot of researchers have used it for robotics and computer vision projects because of its low price while showing great performance. Lately however the Xbox kinect hardware is getting outdated with its low resolution RGB camera and IR based depth perception system which is sensative for other IR light sources. This sensitivty to other IR light sources for examples renders the xbox kinect compelty useless for outdoor projects. Because of these limitations a replecement is needed. This is where the PS4 camera comes into play. 

The PS4 camera has some great hardware upgrades compared to the xbox kinect and is also availbile for a low price. The PS4 camera has a pair of much better 1280x800 resolution cameras paired with a high speed controller. This makes the latency around 120 ~ 150ms. Because of its two cameras the PS4 camera can perceive depth using stereo vision instead of a IR pattern. This makes the PS4 camera also suitable for outdoor projects. The PS4 camera depth image has also a higher resultion which makes it capable of capturaring more detail. 

This repo contains code for using both the PS4 V1(CUH-ZEY1) camera or PS4 V2(CUH-ZEY2) camera with linux. The code in this repo consists a initialization folder which contains code for uploading firmware to the PS4 camera. It also contains code for recieving, viewing and using the RGB and depth stream of the PS4 camera in OpenCV using Python. 

## 2: Installation 

### Hardware
To connect the PS4 camera to a computer first the cable needs to be modded. This is because the PS4 camera has a proprotery connector called the PS4 "AUX" connector. This is actually just a ordinary USB 3.0 cable with a special connector. Because this connector wont fit in a USB 3.0 port of your linux system we need to mod it. This needs to be done by cutting a USB 3.0 cable which has a USB 3.0 type A connector. Also the AUX port on PS4 camera needs to be cut off. After this the USB 3.0 type A connector needs to be solderd to the PS4 camera cable using the colors in the cable. If you have the adapter that allows you to connect the camera to a PS5 using a standard USB 3 connector, this can be used as an alternative to modifying the camera.

For more detailed instructions you can visit:
https://www.instructables.com/HACK-PlayStation-4-Cam-Into-Cheap-3D-Depth-Camera-/

- To check if the cable is made correctly:

- Type in a Terminal ```lsusb```

- This should show a device with the name ```OmniVision Technologies, Inc.```


### Software
Step 1: 
- First we need to install pysub.
- ```sudo pip install --pre pyusb```


Step 2:
- Now we need to initialize the camera by uploading a modded firmware to the PS4 camera. 
- ```cd Firmware_loader```
- ```sudo python3 ps4eye_init.py```
- Select your camera version by typing ```1``` or ```2```
- The program should finish with ```PS4 camera firmware uploaded and device reset``` 


Step 3: 
- Now we need to know at what index the camera has been initalized. 
- Type in a Terminal ```v4l2-ctl --list-devices```
- This should show a device named ```USB Camera-OV580: USB Camera-OV (usb-0000:00:14.0-2):```
- This device will have two  ```/dev/videoX``` locations. 
- The number behind ```video``` will indicate the index. The lowest number of the two is the index we need. 
- Go to ```View_RGB.py``` and ```View_Depth.py``` and change this line with the index number ```cap = cv2.VideoCapture(index number here)```


Step 4: 
Now we can view the Depth or RGB image from the camera. 

- ```cd OpenCV_viewer```

- For RGB run ```python3 View_RGB.py```
- For Depth run ```python3 View_Depth.py```

- If OpenCV gives a error try changing the index number from Step 3

## 3: Changing Video Settings
After using the camera you may find the default video settings of the camera insufficient. The image may be to dark inside or the resolution is not the one you want to use. These settings can be changed by following the steps below.

To change video settings we first need to install the ```v4l2-utils``` package. We can do this with the following command.
- ```sudo apt install v4l2-utils```

Now we can view all available settings with.
- ```v4l2-ctl -l```

To change for example the exposure we can use the following command.
- ```v4l2-ctl exposure = 1```

## 4: Camera specifications
- Latency 120~150ms
- External Dimensions: Approx. 186mm x 27mm x 27mm (width x height x depth) 
- Weight: Approx. 183g 
- Video Pixel: (Maximum) 1280 x 800 pixel x 2 
- Video Frame Rate: 1280x800 pixel @ 60fps 
                     640x400 pixel @ 120fps 
                     320x192 pixel @ 240fps 
- Video Format: RAW YUV (uncompressed) 
- Lens: Dual Lenses, F value/F2.0 fixed focus 
- Capture Range: 30cm~ 
- Field-of-View: 85 degrees 
- Microphone: 4 Channel Microphone Array 
- Connection Type: USB3.0
- Cable Length: Approx. 2m

## 5: References
- This project is a compilation of the amazing work of other people. Big thanks to everyone listed below:
- https://github.com/bigboss-ps3dev
- https://github.com/ps4eye
