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

- ## PROGRAM :
```
Name: NITHISHKUMAR S
Reg NO: 212223240109

import cv2
import matplotlib.pyplot as plt
import numpy as np
# Load the Face Image
faceImage = cv2.imread('IMAGE2.png')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img  width="325" height="397" alt="image" src="https://github.com/user-attachments/assets/1d218321-8cfc-4408-98c9-69fc975abff8" />

```
faceImage.shape
```
<img width="127" height="27" alt="image" src="https://github.com/user-attachments/assets/bce5340a-cf48-498c-9060-adea9990a887" />

```
glassPNG = cv2.imread('GLASS1.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="447" height="293" alt="image" src="https://github.com/user-attachments/assets/75e72a5a-0c8a-4337-b3e6-aeedba5cb068" />


```

# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(680,300))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img  width="625" height="397" alt="image" src="https://github.com/user-attachments/assets/872bd8f3-2411-471c-85ff-9a4657560556" />

```
faceWithGlassesNaive = faceImage.copy()
# Replace the eye region with the sunglass image
faceWithGlassesNaive[450:750,300:980]=glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
```
<img width="325" height="397" alt="image" src="https://github.com/user-attachments/assets/13b21624-6eb0-41dd-a609-f93b821bd9a7" />

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)
# Make a copy
faceWithGlassesArithmetic = faceImage.copy()
# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[450:750,300:980]
# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)
# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

<img  width="825" height="397" alt="image" src="https://github.com/user-attachments/assets/b6d86748-747f-47d7-aad0-17ec49c756ca" />

```

# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[450:750,300:980]=eyeRoiFinal
# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");

```

<img  width="525" height="397" alt="image" src="https://github.com/user-attachments/assets/e923b93b-8349-4ce6-8798-2cf06e8544d0" />


Feel free to fork, contribute, or customize this project for your creative needs!
