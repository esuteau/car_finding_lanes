# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/before_extrapolation/solidWhiteRight.jpg "End Result without Extrapolation"
[image2]: ./test_images_output/solidWhiteRight.jpg "End Result with Extrapolation"
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

Here is my pipeline:
A. Convert the image to gray scale to be able to calculate the gradients with canny edge detection
B. Blur the image using a Gaussian filter
C. Define a specific region of interest around the lane to remove the outside noise
D. Detect the lines using Hough Transform. Try to extract only the longer lines corresponding to the lane limits
E. Extrapolate left and right lines by first spliting the lines into positive and negative slopes,
then by removing the outliers based on a calculation of the mean and standard deviation of the slopes,
 and finally calculating an average of the start and end points for both left and right lines.
F. Combine the original image with the image containing only the lines.

Here is an example before modifying draw_lines()
![alt text][image1]

Here is after modifying draw_lines() to extrapolate the lines.
![alt text][image2]

### 2. Identify potential shortcomings with your current pipeline

The algorithm is highly dependent on a correct definition of the mask, to avoid detecting lines that are not the limits of the lane of consideration.
Therefore it requires the camera to be mounted at a very specific position.
Lane detection was done on fairly straight sections of highways. It seemed to be doing poorly my more pronounced turns...
The draw_lines function uses a hard coded value defining the top section of the mask... This should an argument of the function.

### 3. Suggest possible improvements to your pipeline

It would be nice to find a way to detect the mask automatically without relying on a manual tuning.
The pipeline needs to be enhanced to work on sharp turns.
It should be also tested with different weather and light conditions.

