# 1. Description

This app which uses the deployed cortex APIs as a PaaS captures the frames from a video camera, sends them for inferencing to the cortex APIs, recombines them after the responses are received and then the detections/recognitions are overlayed on the output stream. This is done on the car's dashcam (composed of the Raspberry Pi + GSM module) in real-time. Access to the internet is provided through the GSM module's 4G connection.

The app must be configured to use the API endpoints as shown when calling cortex get yolov3 and cortex get crnn. Checkout how the APIs are defined in their repository.

The app also saves a csv file containing the dates and GPS coordinates of each identified license plate.

# 2. Latency

The observable latency between capturing the frame and broadcasting the predictions in the browser (with all the inference stuff going on) takes about 0.5-1.0 seconds depending on:

How many replicas are assigned for each API.

Internet connection bandwidth and latency.

Broadcast buffer size. To get a smoother stream, use a higher buffer size (10-30) or if you want the stream to be displayed as quickly as possible but with possible dropped frames, go with lower values (<10).

To learn more about how the actual device was constructed, check out this article.
