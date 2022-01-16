---
layout: post
title:  "Converting ndarray to opencv image for tf inference"
date:   2022-01-14 16:30:00 +0200
last_modified_at: 2022-01-14 16:00:00 +0200
permalink: converting-ndarray-to-opencv
description: Converting the numpy array to opencv image for tensorflow inference
published: true
sitemap: true
github_comments_issueid: "7"
categories: opencv numpy tensorflow
---

Below is an example of live semantic segmentation where the segmentation mask is converted from ndarray to opencv image.

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
from IPython.display import clear_output


from tensorflow.python.keras.backend import set_session
graph = tf.get_default_graph()


#Capture the video from the camera

cap = cv2.VideoCapture(0)

while cap.isOpened():
    ret, frame = cap.read()
    #frame2 = frame.reshape((300,480))
    image_resized2 = cv2.resize(frame, (480,320))
    #print(resized.shape)
    #frame2 = np.expand_dims(resized, axis=0)
    
    #Run the Detections using model.predict

    if ret:
        with graph.as_default():
            set_session(sess)
            inputs, predictions = tf_sess.run([tf_input, tf_predictions], feed_dict={
            tf_input: image_resized2[None, ...]
        })
        #cv2.imwrite('file5.jpeg', 255*predictions.squeeze())
        pred_image = 255*predictions.squeeze()

        ##converts pred_image to CV_8UC1 format so that ColorMap can be applied on it
        u8 = pred_image.astype(np.uint8)

        #Color map autumn is applied to the CV_8UC1 pred_image
        im_color = cv2.applyColorMap(u8, cv2.COLORMAP_AUTUMN)
        cv2.imshow('input image', image_resized2)
        cv2.imshow('prediction mask',im_color)
        #cv2.waitKey(0)
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break


    else:
        cap.release()
        break

cap.release()
cv2.destroyAllWindows()
```

The explanation of the individual block is mentioned in the below code 

```
import cv2

from tensorflow.python.keras.backend import set_session
graph = tf.get_default_graph()

with graph.as_default():
    set_session(sess)
    inputs, predictions = tf_sess.run([tf_input, tf_predictions], feed_dict={
    tf_input: image_resized[None, ...]
})

#print("type",type(predictions))
#print(predictions)
#array = np.reshape(array, (1024, 720))
#array = np.reshape(predictions, (320,480))
#array = np.ones([320, 480, 1], dtype=np.float)
#print(array.shape)

#The below block executes in opencv

#------------start block of opencv---------------------------

#cv2.imwrite('file5.jpeg', 255*predictions.squeeze())
pred_image = 255*predictions.squeeze()

##converts pred_image to CV_8UC1 format so that ColorMap can be applied on it
u8 = pred_image.astype(np.uint8)

#Color map autumn is applied to the CV_8UC1 pred_image
im_color = cv2.applyColorMap(u8, cv2.COLORMAP_AUTUMN)

#below line will directly show you the prediction mask without any color map, then you can comment all the 
#above 3 lines. A number of 255 is multiplied because the prediction values are so small and are converted
#to the pixel values from 0-255
#---------------------------------------------------------
#cv2.imshow('img',255*predictions.squeeze())
#---------------------------------------------------------

Below version just shows the mask with the color map.

#---------------------------------------------------------
cv2.imshow('img',im_color)
cv2.waitKey(0)
cv2.destroyWindow('img')
#---------------------------------------------------------

#------------end block of opencv------------------------------

```
