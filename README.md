# License_plate_detection using raspberry pi

This project was inspired by RobertLucian, we want to go through his thought and make it happen use our own training data.
His GitHub address: https://github.com/RobertLucian/cortex-license-plate-reader-client

This is a client for 3(YOLOv3, CRAFT text detector, CRNN text recognizer) cortex-deployed ML models. 

## 1.1 Description

This app which uses the deployed cortex APIs as a PaaS captures the frames from a video camera, sends them for inferencing to the cortex APIs, recombines them after the responses are received and then the detections/recognitions are overlayed on the output stream. This is done on the car's dashcam (composed of the Raspberry Pi + GSM module) in real-time. Access to the internet is provided through the GSM module's 4G connection.

The app must be configured to use the API endpoints as shown when calling cortex get yolov3 and cortex get crnn. Checkout how the APIs are defined in their repository.

The app also saves a csv file containing the dates and GPS coordinates of each identified license plate.

### 1.2 Latency

The observable latency between capturing the frame and broadcasting the predictions in the browser (with all the inference stuff going on) takes about 0.5-1.0 seconds depending on:

* How many replicas are assigned for each API.

* Internet connection bandwidth and latency.

* Broadcast buffer size. To get a smoother stream, use a higher buffer size (10-30) or if you want the stream to be displayed as quickly as possible but with possible dropped frames, go with lower values (<10).

### 1.3 Target Machine

* Target machine 1: Raspberry Pi
* Target machine 2: [Raspberry pi camera Board v2-8 Megapixels](https://www.amazon.com/Raspberry-Pi-Camera-Module-Megapixel/dp/B01ER2SKFS) $29.95

## 2 Prediction Model and DATA
### 2.1 Model 
#### 2.1.1 YOLOv3

[YOLOv3](https://pjreddie.com/darknet/yolo/) is the most quickest model right now and have a pretty good mAP, we will use this model to detect object. 
We picked one model which use Keras to relize
* Keras: https://github.com/experiencor/keras-yolo3

#### 2.1.2 CRAFT text detector, which can detect texts in our object
#### 2.1.3 CRNN Rucurrent neural network, the purpose is to form the text to a word, so it has to be RNN model

Robert find a keras-ocr package, which packaged CRAFT and CRNN, very useful, so we decide to use the model. 
* keras-ocr: https://github.com/faustomorales/keras-ocr

### 2.2 Data
#### To do list
- [ ] record video
- [ ] Use VOTT to label and pick the pictures which contain plate, about 1000 images

We decide to record videos in our city and use VOTT to label all with license plates. The target is 1000 images
* VOTT: https://github.com/microsoft/VoTT
