# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features: 
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program 
```
import cv2
import matplotlib.pyplot as plt
import numpy as np

faceImage = cv2.imread('passport.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
![a1](https://github.com/user-attachments/assets/e06ae7e9-6725-44cd-a38e-e8144a4af527)

```
glassPNG = cv2.imread('glasses.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
![a2](https://github.com/user-attachments/assets/979a3e53-f742-447f-9b14-340e616f6765)

```
glassPNG = cv2.resize(glassPNG, (550,140))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![a3](https://github.com/user-attachments/assets/69dc5477-50c6-4a10-9cf1-ea39e87edad8)

```
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[425:565, 146:696] = glassBGR 
plt.imshow(faceWithGlassesNaive[...,::-1])
```
![a4](https://github.com/user-attachments/assets/55c82903-0dad-48ea-a365-fe699e299cef)

```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI= faceWithGlassesArithmetic[425:565, 146:696]
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
maskedGlass = cv2.multiply(glassBGR,glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
![a5](https://github.com/user-attachments/assets/44df1420-3b08-432d-8e8c-4d91ec9d61bb)

```
faceWithGlassesArithmetic[425:565, 146:696]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
![a6](https://github.com/user-attachments/assets/ce08e799-f645-42c2-9978-06ba0694ee76)
