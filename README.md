# License-Plate-Detection-using-Raspberry-PI4-YOLOV3
Iranian ALPR  task using YOLOV3 (Pytorch)  on Raspberry-Pi 4

## Discription about Project
according to last project in github repo about detecting iranian license-plate detection(LPD) using yolov3 in [Repo](https://github.com/behnoudshafizadeh/iranian-LPR-using-deep-learning-algorithm), we decide to employ that on Raspberri-Pi 4 to illustrate the functionality of LPD on real world. moreover, we provide a structure of deep learning algorithm trained before and tested on different types of License-Plate(LP) in images to investigate the being real-time of our system. in below, see our raspberry pi :

https://user-images.githubusercontent.com/53394692/130784360-bc05d675-4cbd-46aa-b924-d1630d7702c3.mp4

## overal architecture
basis on architecture, the raspberri-Pi receive input image containing a vehicle, then using first `YOLOv3` algorithm to detect the possible LP in it, after that, since we will have the coordinates of LPs which lead to `crop` from region and passed to another `YOLOv3` algorithm to earn possible characters in LP. finally, we use the characters in ordinary numbers to search it in our Query datebase. if the LP number in the list, the `green LED` will be starting to trun on (it means `allow`) else the `red LED` will be turned on (it means `not allow`).

![general architecture](https://user-images.githubusercontent.com/53394692/130901195-fceeb371-e9eb-4465-803e-f9977b033856.PNG)


## Requirements
* Raspberry-pi 4B (Hardware)
> you see the architecture of raspberry 4 and its different pins for using input/output task. furthermore, for using in `python` we need import `GPIO` package to use their functions, for instanc, we set `pin #24` as output to turn on `LED`.
![raspberri4 architecture](https://user-images.githubusercontent.com/53394692/130900285-9e1925cc-c59f-43b4-8a1e-59e62b86699a.png)![input-output Pins](https://user-images.githubusercontent.com/53394692/130900643-614a7421-af38-41e7-8eaa-449ba06d0e29.png)

* install Raspbian (OS on Hardware)
> due to use of raspberry Pi, you will be needing an `OS` like a (windows) to employ its properties and features on it,so by using this [install link](https://www.raspberrypi.org/documentation/computers/getting-started.html) you can install your environment. see the results of configuration, in below figure: 

![configuration os](https://user-images.githubusercontent.com/53394692/130903437-17b54c17-64c1-429a-b2b5-1b2cd4921657.png)

* following packages are needed to set our configuration for employing the `yolov3` algorithm and an `image processing` step:
```
command for installing : pip install <package name>
numpy
torch >= 1.3
matplotlib
pycocotools
tqdm
Pillow
declxml==0.9.1

```
> Notice : for installing opencv, use this [link](https://www.pyimagesearch.com/2019/09/16/install-opencv-4-on-raspberry-pi-4-and-raspbian-buster/).

* Test Procedure
> in the below fiure, you see the structure of main folder which cause the ALPR implementation. following files 

![alpr](https://user-images.githubusercontent.com/53394692/130906995-feab27cd-5182-4cdd-b79d-3a9b31077d7a.png)

```
output directory : the results of first yolov3 for LP detection
output1 directory : the results of second yolov3 for CR recognition
utils directory : packages and fuctions used in yolov3 algorithms
convertedlp.weights : weights (before trained) for LP detection
convertedch.weights : weights (before trained) for CR recognition
crop.py : code for cropping detected LPs from image
detect.py : main code using yolov3 strucrue for detecting objects
LED.py : using python packages for accessing LED on raspberry Pi
models.py : the structure of yolov3 neural network (activatation fuction, upsampling fuction, ...)
objectlp.names : labels in LP detection
objecttochar.names : labels in CR detection
output.py : instructions for reading characters from detected LPs and turning on LEDs basis on our LPs number
test.jpg : input image
test2.jpg : cropped LPs as an input for second yolov3
yolov3-1cls.cfg : configuration file for designing the layers in LP yolov3 neural network 
yolov3-1clstochar.cfg : configuration file for designing the layers in CR yolov3 neural network
test.sh : bash script file

```
* summarization
> for running all of above mentioned as an unique structure, we gather all oof them together in bash script file as `test.sh`. in primary step, we set a input image `test.jpg` in the directory ,then we run bash file to employ all of instructions sequentially (by order). in the first line we use an instruction for implementing LP yolov3 that it extract possibe LPs and their coordinations in image as a `.txt` file in `output` directory. in seconde instruction, `crop.py` used to extract LPs from input image in `output` directory, and then a third line employ a seconde yolov3 for detecting possible characters and their coordinations (`.txt` file) in LPs and save the results in `output1` directory. in finally step, using `output.py` code for reading LP number. 

  * write `./test.sh` to run bash file, and see the results as below (there is an aexample when the LP is not in Query database) :
![sample1](https://user-images.githubusercontent.com/53394692/130915835-3a01efe1-33d9-45e2-a7a4-6bec52209a7f.PNG)
![finall bash result](https://user-images.githubusercontent.com/53394692/130915332-a5d15440-59cd-4cb6-b59b-89286c64521c.PNG)
> you see, the LED show red light in it, when we have not LP number is `ls` list :

https://user-images.githubusercontent.com/53394692/130777391-9040bdbb-c404-418f-9fae-d1598599dd83.mp4

> otherwise, the LED show green light while you have the LP in `ls` list : 

https://user-images.githubusercontent.com/53394692/130783385-43e91cd0-071f-4af4-97f4-f70b06e06865.mp4


## LICENSE
> this project was done by me `behnoud shafizadeh` and my co-workers `ehsan ramzani` and `navid pourhadi` in the kharazmi university lab, supervised by `DR.Farshad Eshghi` and `DR.Manoochehr KelarEstaghi`,so the full source of code and dataset in this project are out authority and related to `kharazmi university of tehran`,so if you would like to contiribute with our group and access to out document,please contact with our emails : `behnud.shafizadeh@gmail.com` and `npourhadi1998@gmail.com`,thanks for your consideration.

