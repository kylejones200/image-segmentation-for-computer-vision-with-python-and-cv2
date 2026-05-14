---
author: "Kyle Jones"
date_published: "January 1, 2024"
date_exported_from_medium: "November 10, 2025"
canonical_link: "https://medium.com/@kyle-t-jones/image-segmentation-for-computer-vision-with-python-and-cv2-a07a0f70b79d"
---

# Image Segmentation for Computer Vision with Python and CV2 Image Segmentation is the process of dividing an image into multiple
regions or segments, each of which corresponds to a different object...

### Image Segmentation for Computer Vision with Python and CV2 

#### Image Segmentation is the process of dividing an image into multiple regions or segments, each of which corresponds to a different object or part of the image. The goal of image segmentation is to simplify and/or change the representation of an image into something that is more meaningful and easier to analyze.
Image Segmentation is a fundamental task in computer vision and is used in many applications, such as object recognition, image analysis, and medical imaging. Image segmentation is like identifying the different objects in a picture and drawing lines around them. For example, in a photograph of a person in front of a building, image segmentation would identify the person and the building as two separate regions.

This project assumes that you already have a background in computer vision. If you are looking for something simplier, check out my intro to computer vision article.

[Introduction to Deep Learning for computer vision with Python\ *Deep learning has achieved significant breakthroughs in a wide range of applications, including image and speech...*medium.com](https://medium.com/@kylejones_47003/introduction-to-deep-learning-for-computer-vision-with-python-85f94acc3a6b "https://medium.com/@kylejones_47003/introduction-to-deep-learning-for-computer-vision-with-python-85f94acc3a6b")[](https://medium.com/@kylejones_47003/introduction-to-deep-learning-for-computer-vision-with-python-85f94acc3a6b) There are various techniques for image segmentation, including thresholding, edge detection, and clustering. Thresholding involves setting a threshold value and separating pixels based on their intensity values. Edge detection involves detecting the edges or boundaries between regions in an image. Clustering involves grouping pixels based on their similarity in color, texture, or other features.

Once an image has been segmented, it is often possible to extract useful information from each region. For example, we may want to measure the size, shape, or color of each object in an image. This information can then be used for various purposes, such as identifying objects in a scene or detecting abnormalities in medical images.

Overall, image segmentation is an essential task in computer vision that allows us to analyze images and extract meaningful information from them. It is a complex process, but there are many tools and techniques available to make it easier, even for beginners.

#### Forms of Image Segmentation
There are two main forms of image segmentation:

Semantic segmentation: Semantic segmentation is the process of labeling each pixel in an image with a class label, such as object, background, or boundary. The goal of semantic segmentation is to assign a meaningful label to each pixel in the image, based on its context and surrounding pixels. This is useful for various applications, such as object detection, scene understanding, and autonomous driving.

Instance segmentation: Instance segmentation is the process of separating each individual object instance in an image and assigning a unique label to it. Unlike semantic segmentation, instance segmentation differentiates between multiple instances of the same object class, such as identifying each person in a crowd. This is useful for applications such as robotics, where individual object instances need to be identified and tracked.

In other words, local segmentation and global segmentation are two different approaches to image segmentation that vary in the scope of the segmentation.

Local segmentation is the process of segmenting an image into regions based on local image features such as texture, color, or intensity. This means that the segmentation is performed on small, localized regions of the image, without taking into account the larger context of the image. Local segmentation is useful for applications such as object recognition, where local image features are often more informative than global features.

Global segmentation, on the other hand, is the process of segmenting an image into regions based on the overall context and structure of the image. This means that the segmentation is performed on the entire image as a whole, taking into account the relationships between different parts of the image. Global segmentation is useful for applications such as scene understanding, where the overall structure of the scene is important.

Both local and global segmentation have their own strengths and weaknesses, and the choice of which approach to use depends on the specific application and the characteristics of the images being segmented. In some cases, a combination of both approaches may be used to achieve the best results.

#### Types of Image Segmentation Techniques
There are several types of image segmentation techniques, some of which are listed below:

Thresholding: This is a simple image segmentation technique that involves separating pixels based on their intensity values. A threshold value is set, and pixels above or below the threshold are segmented into different regions.

Edge-based segmentation: This technique involves detecting the edges or boundaries between different regions in an image. The edges can be detected using various algorithms, such as the Sobel, Canny, or Laplacian edge detection algorithms.

Region-growing segmentation: This technique involves starting with an initial seed pixel and growing the region by including neighboring pixels that have similar properties, such as intensity or color.

Clustering-based segmentation: This technique involves grouping pixels into clusters based on their similarity in color, texture, or other features. The most common clustering algorithm used for image segmentation is the k-means algorithm.

Watershed segmentation: This technique involves treating an image as a topographic map and simulating the flooding of the landscape. Watersheds, or areas of high elevation, are separated by ridges, or areas of low elevation.

Graph-based segmentation: This technique involves representing an image as a graph, where each pixel is a node and the edges represent the similarity between neighboring pixels. The graph is then partitioned into different regions using various algorithms, such as the normalized cuts algorithm.

These are just a few examples of the many techniques available for image segmentation. The choice of which technique to use depends on the specific application and the characteristics of the images being segmented.

#### Thresholding
There are several different thresholding techniques that can be used, depending on the characteristics of the image being segmented. The most common thresholding techniques are:

Global thresholding: This involves setting a single threshold value for the entire image. Pixels with intensity values above the threshold are segmented as foreground, while pixels with intensity values below the threshold are segmented as background.

Adaptive thresholding: This technique is useful when the lighting conditions in an image vary significantly. Adaptive thresholding involves calculating a threshold value for each pixel based on the local image intensity values. This can result in more accurate segmentation of the foreground and background regions.

Otsu's thresholding: This technique involves finding an optimal threshold value that maximizes the separation between foreground and background pixels. This is achieved by minimizing the intra-class variance of the intensity values for each class.

Thresholding is a simple but effective technique that can be used for a wide range of applications, such as object detection, image analysis, and image processing. However, it can be sensitive to variations in lighting conditions and may not be suitable for images with complex or variable backgrounds.

#### Global thresholding
In thresholding, each pixel value is compared with the threshold value. If the pixel value is smaller than the threshold, it is set to 0, otherwise, it is set to a maximum value (generally 255). Thresholding is a very popular segmentation technique, used for separating an object considered as a foreground from its background.

It is a simple image segmentation technique that involves setting a single threshold value for the entire image, and then segmenting pixels based on their intensity values. Here's an example of how to perform global thresholding using OpenCV in Python (note the \`OpenCV\` module is named cv2).

```python
import cv2
from google.colab.patches import cv2_imshow
import matplotlib.pyplot as plt
# Load image from file
image1 = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Calender.jpg')
img = cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY)
# Apply global thresholding
thresh_value, thresh_image = cv2.threshold(img, 120, 255, cv2.THRESH_BINARY)
#print(thresh_value)
fig, axs = plt.subplots(1, 2)
# Display the Thresholded images in subplots
axs[0].imshow(img)
axs[0].set_title('Original Image')
axs[1].imshow(thresh_image)
axs[1].set_title('Thresh Binary Image')
# Hide x and y ticks for all subplots
for ax in axs.flat:
 ax.set_xticks([])
 ax.set_yticks([])
# Display image in notebook
plt.show()
```


<figcaption>Binary thresholding using OpenCV. Source: Author.</figcaption>


Let's unpack this a bit.

Syntax: cv2.threshold(source, thresholdValue, maxVal, thresholdingTechnique)

Parameters:

- source: Input Image array (must be in Grayscale which is the default in cv2).
- thresholdValue: Value of Threshold below and above which pixel values will change accordingly.
- maxVal: Maximum value that can be assigned to a pixel.
- thresholdingTechnique: The type of thresholding to be applied.

#### Simple Thresholding Techniques
The basic Thresholding technique is Binary Thresholding. For every pixel, the same threshold value is applied. If the pixel value is smaller than the threshold, it is set to 0, otherwise, it is set to a maximum value.

The different Simple Thresholding Techniques are:

cv2.THRESH_BINARY: If pixel intensity is greater than the set threshold, value set to 255, else set to 0 (black).

cv2.THRESH_BINARY_INV: Inverted or Opposite case of cv2.THRESH_BINARY.

cv.THRESH_TRUNC: If pixel intensity value is greater than threshold, it is truncated to the threshold. The pixel values are set to be the same as the threshold. All other values remain the same.

cv.THRESH_TOZERO: Pixel intensity is set to 0, for all the pixels intensity, less than the threshold value.

cv.THRESH_TOZERO_INV: Inverted or Opposite case of cv2.THRESH_TOZERO.

```python
import cv2
import matplotlib.pyplot as plt
# Load image from file
image1 = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Calender.jpg')
img = cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY)
# Apply global thresholding
thresh_value, thresh_binary_INV = cv2.threshold(img, 120, 255, cv2.THRESH_BINARY_INV)
thresh_value1, thresh_trunc = cv2.threshold(img, 120, 255, cv2.THRESH_TRUNC)
thresh_value2, thresh_toZero = cv2.threshold(img, 120, 255, cv2.THRESH_TOZERO)
thresh_value3, thresh_toZeroINV = cv2.threshold(img, 120, 255, cv2.THRESH_TOZERO_INV)

#print(thresh_value)
fig, axs = plt.subplots(2, 2)
# Display the Thresholded images in subplots
axs[0,0].imshow(thresh_binary_INV)
axs[0,0].set_title('Thresh Binary Inv Image')
axs[0,1].imshow(thresh_trunc)
axs[0,1].set_title('Thresh Trunc Image')
axs[1,0].imshow(thresh_toZero)
axs[1,0].set_title('Thresh to Zero Image')
axs[1,1].imshow(thresh_toZeroINV)
axs[1,1].set_title('Thresh to Zero INV Image')
# Hide x and y ticks for all subplots
for ax in axs.flat:
 ax.set_xticks([])
 ax.set_yticks([])
# Display image in notebook
plt.show()
```


<figcaption>Thresholding examples using OpenCV. Source: Author.</figcaption>


In the code above, we first read in an image using the cv2.imread() and convert it as grayscale cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY) function.

We then apply global thresholding using the cv2.threshold() function, which takes in the input image, the threshold value (120 in this case), the maximum value (255 in this case), and the thresholding type (cv2.THRESH_BINARY in this case, which means that pixels above the threshold value are set to 255, while pixels below the threshold value are set to 0). The function returns the threshold value and the thresholded image.

Finally, we display the original image and the thresholded images using plt.show() functions.

Note that the threshold value of 120 used in this example is a fixed value that may not work well for all images. In practice, it's often necessary to experiment with different threshold values to find the best one for a particular image.

#### Adaptive thresholding
It is a technique for segmenting an image into foreground and background regions by calculating a local threshold value for each pixel. The basic idea behind adaptive thresholding is to compute a threshold value for each pixel based on the local intensity distribution in its surrounding neighborhood. This approach can be particularly useful when the lighting conditions in the image vary significantly.

Here's an example of how to perform adaptive thresholding using OpenCV in Python:

```python
import cv2
# Read the image in grayscale
image1 = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Calender.jpg')
img = cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY)
# Apply adaptive thresholding
ADP_thresh_image = cv2.adaptiveThreshold(img, 255, cv2.ADAPTIVE_THRESH_MEAN_C, cv2.THRESH_BINARY, 11, 2)
ADP_thresh_Gaussian = cv2.adaptiveThreshold(img, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY, 199, 5)
fig, axs = plt.subplots(2, 2)
# Display the Thresholded images in subplots
axs[0,0].imshow(img)
axs[0,0].set_title('Original Image')
axs[0,1].imshow(ADP_thresh_image)
axs[0,1].set_title('Adaptive Thresholded MEAN')
axs[1,0].imshow(ADP_thresh_Gaussian)
axs[1,0].set_title('Adaptive Thresholded Gaussian')
# Hide x and y ticks for all subplots
for ax in axs.flat:
 ax.set_xticks([])
 ax.set_yticks([])
# Display image in notebook
plt.show()
```


<figcaption>Adaptive thresholding examples using OpenCV. Source: Author.</figcaption>


cv2.ADAPTIVE_THRESH_MEAN_C: Threshold Value = (Mean of the neighborhood area values --- constant value). In other words, it is the mean of the blockSize×blockSize neighborhood of a point minus constant.

cv2.ADAPTIVE_THRESH_GAUSSIAN_C: Threshold Value = (Gaussian-weighted sum of the neighborhood values --- constant value). In other words, it is a weighted sum of the blockSize×blockSize neighborhood of a point minus constant.

thresholdType: The type of thresholding to be applied.

blockSize: Size of a pixel neighborhood that is used to calculate a threshold value.

constant: A constant value that is subtracted from the mean or weighted sum of the neighborhood pixels.

We applied adaptive thresholding using the cv2.adaptiveThreshold() function, which takes in the input image, the maximum value (255 in this case), the adaptive thresholding method (cv2.ADAPTIVE_THRESH_MEAN_C in this case, which computes the threshold value as the mean of the surrounding pixel values), the thresholding type (cv2.THRESH_BINARY in this case), the block size (11 in this case, which is the size of the local neighborhood around each pixel used for computing the threshold value), and a constant value subtracted from the mean (2 in this case). The function returns the thresholded image.

Note that the block size used in adaptive thresholding determines the size of the local neighborhood around each pixel used for computing the threshold value. Larger block sizes will result in smoother thresholding, but may miss small details in the image. It's often necessary to experiment with different block sizes to find the best one for a particular image.

#### Otsu's thresholding
It is a technique for automatically finding the optimal threshold value for image segmentation. It works by maximizing the variance between two classes of pixels, foreground and background, based on the gray-level histogram of the image. This approach can be particularly useful when the image has a bimodal histogram, where the foreground and background pixels have distinct gray-level distributions.

Here's an example of how to perform Otsu's thresholding using OpenCV in Python:

```python
import cv2
# Read the image in grayscale
image1 = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Bimodal_img_1.jpeg')
img = cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY)
# Apply Otsu's thresholding
ret, thresh_image = cv2.threshold(img, 0, 255, cv2.THRESH_BINARY+cv2.THRESH_OTSU)
fig, axs = plt.subplots(1, 2)
# Display the Thresholded images in subplots
axs[0].imshow(img)
axs[0].set_title('Original Image')
axs[1].imshow(thresh_image)
axs[1].set_title('OTSU Thresh Image')
# Hide x and y ticks for all subplots
for ax in axs.flat:
 ax.set_xticks([])
 ax.set_yticks([])
# Display image in notebook
plt.show()
```


<figcaption>Otsu’s thresholding using OpenCV. Source: Author.</figcaption>


We applied Otsu's thresholding using the cv2.threshold() function, which takes in the input image, the minimum threshold value (0 in this case), the maximum threshold value (255 in this case), the thresholding type (cv2.THRESH_BINARY+cv2.THRESH_OTSU in this case, which applies Otsu's thresholding method), and returns the thresholded image along with the threshold value computed by Otsu's method (ret in this case).

Note that Otsu's thresholding method assumes that the image has a bimodal histogram, with two distinct peaks corresponding to the foreground and background pixels. If the image has a unimodal histogram, with only one peak, Otsu's method may not work well.

Let's see our image has bimodal histogram or not?

```python
import cv2
from matplotlib import pyplot as plt
# Read the image in grayscale
image1 = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Bimodal_img_1.jpeg')
img = cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY)
# Calculate the histogram
hist = cv2.calcHist([img], [0], None, [256], [0, 256])
# Plot the histogram
plt.plot(hist, color='gray')
plt.xlabel('Intensity Value')
plt.ylabel('Pixel Count')
plt.show()
```


Syntax: cv2.threshold(source, thresholdValue, maxVal, thresholdingTechnique)

Parameters:

source: Input Image array (must be in Grayscale).

thresholdValue: Value of Threshold below and above which pixel values will change accordingly.

maxVal: Maximum value that can be assigned to a pixel.

thresholdingTechnique: The type of thresholding to be applied.

### Edge-based segmentation
It is a technique in which image regions are segmented based on edges, or boundaries, in the image. The basic idea behind edge-based segmentation is that the boundaries between different regions in an image are typically characterized by sharp changes in intensity, color, or texture. By detecting these boundaries, it is possible to segment an image into different regions.

Canny, Sobel, and Laplacian are popular algorithms for edge detection in computer vision and image processing. Here's a brief explanation of when and why each algorithm is used:

Canny Edge Detection: The Canny edge detector is a multi-stage algorithm that is known for its high accuracy and low error rate. It is often used in applications where precise detection of edges is required, such as in object recognition, tracking, and segmentation. The Canny algorithm is computationally expensive, but its accuracy and low error rate make it an excellent choice for high-precision applications.

Sobel Edge Detection: The Sobel operator is a simple algorithm for detecting edges in an image. It calculates the gradient of the image intensity in the x and y directions, which can be combined to produce the edge magnitude and orientation. The Sobel algorithm is computationally efficient and can be used in real-time applications such as video processing and robotics.

Laplacian Edge Detection: The Laplacian operator is another popular algorithm for edge detection. Unlike the Sobel and Canny algorithms, the Laplacian operator is a second-order differential operator that detects edges based on the zero-crossings of the second derivative of the image intensity function. The Laplacian operator is sensitive to noise, and its results may require additional filtering or processing to obtain accurate edge detection.

In summary, the choice of edge detection algorithm depends on the specific application requirements, including the desired accuracy, speed, and computational resources. The Canny algorithm is an excellent choice for high-precision applications, while the Sobel algorithm is faster and suitable for real-time applications. The Laplacian algorithm is less commonly used due to its sensitivity to noise, but it can be effective when combined with additional filtering or processing.

#### Canny Edge Detector
The Canny edge detector works by first smoothing the image with a Gaussian filter to remove noise. Then, it computes the gradient of the image using a Sobel filter, which highlights areas of the image with high intensity changes. Finally, it applies non-maximum suppression and hysteresis thresholding to extract the edges.

Here's an example of how to perform edge-based segmentation using the Canny edge detector in OpenCV:

```python
import cv2
import numpy as np
# Read the image
img = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Calender.jpg')
# Convert the image to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
# Apply Gaussian smoothing to remove noise
blur = cv2.GaussianBlur(gray, (5, 5), 0)
# Apply Canny edge detection
edges = cv2.Canny(blur, 100, 200)
fig, axs = plt.subplots(1, 2)
# Display the Thresholded images in subplots
axs[0].imshow(img)
axs[0].set_title('Original Image')
axs[1].imshow(edges)
axs[1].set_title('Edgy Image')
# Hide x and y ticks for all subplots
for ax in axs.flat:
 ax.set_xticks([])
 ax.set_yticks([])
# Display image in notebook
plt.show()
```


<figcaption>Canny edge image using cv2. Source: Author.</figcaption>


We applied Gaussian smoothing using the \`cv2.GaussianBlur()\` function to remove noise from the image. Then, we applied Canny edge detection using the \`cv2.Canny()\` function with lower and upper threshold values of 100 and 200, respectively.

#### Sobel Edge Detector
The Sobel operator is a widely used algorithm for edge detection. It works by calculating the gradient of the image intensity function, which highlights areas of the image with high intensity changes.

Here's an example of how to use the Sobel operator for edge detection in OpenCV using Python:

```python
import cv2
import numpy as np
# Read the image
img = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Calender.jpg')
# Convert the image to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
# Apply Sobel edge detection in the x direction
sobelx = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3)
# Apply Sobel edge detection in the y direction
sobely = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3)
# Combine the x and y gradients
sobel = cv2.addWeighted(sobelx, 0.5, sobely, 0.5, 0)
# Display the original image and the edges
fig, axs = plt.subplots(1, 2)
# Display the Thresholded images in subplots
axs[0].imshow(img)
axs[0].set_title('Original Image')
axs[1].imshow(sobel)
axs[1].set_title('Sobel Edgy Image')
# Hide x and y ticks for all subplots
for ax in axs.flat:
 ax.set_xticks([])
 ax.set_yticks([])
# Display image in notebook
plt.show()
```


<figcaption>Sobel edge image using cv2. Source: Author.</figcaption>


We applied the Sobel operator using the \`cv2.Sobel()\` function, specifying the direction of the gradient as either horizontal (x) or vertical (y) by setting the appropriate arguments to 1 and 0, respectively. The ksize argument specifies the size of the Sobel kernel.

We then combined the x and y gradients using the \`cv2.addWeighted()\` function, with equal weighting for each gradient.

#### Laplacian Edge Detector
Unlike the Sobel and Canny algorithms, the Laplacian operator is a second-order differential operator that detects edges based on the zero-crossings of the second derivative of the image intensity function.

Here's an example Python code for Laplacian edge detection using OpenCV:

```python
import cv2
import numpy as np
# Read the image
img = cv2.imread('/content/drive/MyDrive/Colab Notebooks/Images/Calender.jpg')
# Convert the image to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
# Apply Laplacian edge detection
laplacian = cv2.Laplacian(img, cv2.CV_64F)
# Convert the result to uint8 format
laplacian_edges = cv2.convertScaleAbs(laplacian)
# Display the original image and the edges
fig, axs = plt.subplots(1, 2)
# Display the Thresholded images in subplots
axs[0].imshow(img)
axs[0].set_title('Original Image')
axs[1].imshow(laplacian_edges)
axs[1].set_title('Laplacian Edgy Image')
# Hide x and y ticks for all subplots
for ax in axs.flat:
 ax.set_xticks([])
 ax.set_yticks([])
# Display image in notebook
plt.show()
```


<figcaption>Laplacian edge image using cv2. Source: Author.</figcaption>


We applied the Laplacian operator using \`cv2.Laplacian()\`. The second argument, cv2.CV_64F, specifies the data type of the output image, which in this case is a 64-bit floating-point number.

Since the output image is in floating-point format, we need to convert it to uint8 format before displaying it. We use \`cv2.convertScaleAbs()\` for this purpose, which performs an absolute value operation followed by a scaling operation to convert the data type.

In the same way, there are other segmentation techniques that can be used according to the requirements.

[Object Detection with Python using OpenCV: Introduction to computer vision\ *Object detection is a computer vision task that involves detecting and localizing objects within an image. This task is...*medium.com](https://medium.com/@kylejones_47003/object-detection-with-python-using-open-cv-introduction-to-computer-vision-74508c39191d "https://medium.com/@kylejones_47003/object-detection-with-python-using-open-cv-introduction-to-computer-vision-74508c39191d")[](https://medium.com/@kylejones_47003/object-detection-with-python-using-open-cv-introduction-to-computer-vision-74508c39191d)
### Related Stories
- [[Intro to Computer Vision with OpenCV in Python](https://medium.com/@kylejones_47003/intro-to-computer-vision-with-opencv-in-python-628eb9fca2db)]
- [[Object Detection with Python using OpenCV: Introduction to computer vision](https://medium.com/@kylejones_47003/object-detection-with-python-using-open-cv-introduction-to-computer-vision-74508c39191d)]
- [[Introduction to Deep Learning for computer vision with Python](https://medium.com/@kylejones_47003/introduction-to-deep-learning-for-computer-vision-with-python-85f94acc3a6b)]
