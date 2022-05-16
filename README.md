
# Captcha Cracking

[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/tterb/atomic-design-ui/blob/master/LICENSEs)

This is a program aiming to crack some CAPTCHA of several websites made by training a deep learning method.




## Introduction 

#### What is Captcha (Completely Automated Public Turing test to Tell Computers and Humans Apart)?

According to Wikipedia, a CAPTCHA is a type of challenge–response test used in computing to determine whether or not the user is human.


#### How does a CAPTCHA work?

The idea is that a computer program such as a bot will be unable to interpret the distorted letters, while a human being, who is used to seeing and interpreting letters in all kinds of contexts – different fonts, different handwritings, etc. – will usually be able to identify them.

CAPTCHAs were designed to prevent computers from automatically filling out forms by verifying that you are a real person. But with the rise of deep learning and computer vision, they can now often be defeated easily.


## Overview of Captcha cracking
- Datasets and Data-Loading
- Image Preprocessing
- Model creation
- Validation
- Prediction
### Datasets and Data-Loading

Dataset was collected from www.It contains 1040 captcha image of sizw ___.

### Image Preprocessing

The aim of pre-processing is an improvement of the image data that suppresses undesired distortions or enhances some image features relevant for further processing and analysis task.

It includes:
- Greyscale conversion
- 90 degree clockwise rotation
- Adaptive Thresholding
- Opening(MorphologyEx)
- dilate
- Gaussian blur


#### Greyscale conversion

Converting to greyscale will help in sharpening the image by identifying the light and dark areas.

![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/grayscale_captcha.png)

#### 90 degree clockwise rotation
Rotating image 90 degree clockwise.

#### Adaptive Thresholding

Adaptive thresholding is the method where the threshold value is calculated for smaller regions. This leads to different threshold values for different regions with respect to the change in lighting. 

![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/aadaptivethresholdingcaptcha.png)

#### Opening(MorphologyEx())

Opening is just another name of erosion followed by dilation. It is useful in removing noise, as we explained above. Here we use the function, cv.morphologyEx()
- Erosion : It erodes away the boundaries of foreground object (Always try to keep foreground in white). So what it does? The kernel slides through the image (as in 2D convolution). A pixel in the original image (either 1 or 0) will be considered 1 only if all the pixels under the kernel is 1, otherwise it is eroded (made to zero). It is useful for removing small white noises 
![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/morphx_captcha.png)

#### Dilation
It is just opposite of erosion. Here, a pixel element is '1' if atleast one pixel under the kernel is '1'. So it increases the white region in the image or size of foreground object increases. Normally, in cases like noise removal, erosion is followed by dilation. Because, erosion removes white noises, but it also shrinks our object. So we dilate it. Since noise is gone, they won't come back, but our object area increases. It is also useful in joining broken parts of an object.
![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/dilate_cpatcha.png)

#### Gaussian blur 
Image blurring is achieved by convolving the image with a low-pass filter kernel. It is useful for removing noise. It actually removes high frequency content (eg: noise, edges) from the image. So edges are blurred a little bit in this operation (there are also blurring techniques which don't blur the edges).Here a Gaussian kernel is used.Gaussian blurring is highly effective in removing Gaussian noise from an image.
![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/gaussina_blur_captcha.png)

### Model building and training
#### Model Architecture
![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/captcha_model.png)


#### Loss function

Connectionist Temporal Classification (CTC) loss :
Connectionist Temporal Classification (CTC) is a type of Neural Network output helpful in tackling sequence problems like handwriting and speech recognition where the timing varies. Using CTC ensures that one does not need an aligned dataset, which makes the training process more straightforward.

![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/training_epoch.png)

ref: 1,https://distill.pub/2017/ctc/ , 2,https://sid2697.github.io/Blog_Sid/algorithm/2019/10/19/CTC-Loss.html
3,https://stackoverflow.com/questions/57292896/understanding-ctc-loss-for-speech-recognition-in-keras
4,https://towardsdatascience.com/intuitively-understanding-connectionist-temporal-classification-3797e43a86c

### validation 

![alt text](https://raw.githubusercontent.com/vivekalex61/captcha_cracking/main/images/evaluation_capt.png)

## Predictions


## End Notes
The model is not finetuned. 
