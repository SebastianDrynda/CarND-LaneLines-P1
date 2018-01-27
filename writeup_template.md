# **Finding Lane Lines on the Road** 

## Reflection

## 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The image pipeline consists on 6 steps: 

**Image Pipeline step 1: Converting images into gray scale**
def image_pipeline_gray(image) 
Returns a gray scaled version of the input image using cv2.cvtColor method.

###Image Pipeline step 2: Applying Gaussian smoothing
def image_pipeline_gaussian_blur(image)
Applies a Gaussian blur to the provided image using cv2.GaussianBlur method

###Image Pipeline step 3: Applying Canny transform
def image_pipeline_canny(image)
Use a Canny transformation to find edges on the image using cv2.Canny method.

###Image Pipeline step 4: Applying Region of Interest
def image_pipeline_roi(image)
Masks the image segments that are not interesting in regards to the line detection

###Image Pipeline step 5: Applying Hough transform
def image_pipeline_hough(image)
Use the Hough transformation to find the lines on the masked image using cv2.cv2.HoughLinesP. 

###Image Pipeline step 6: Merging original image with Hough transform lines
def weighted_img(image)
Merges the output of hough transformation with the original image to represent the lines on it.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
separating line segments by their slope to decide which segments are part of the left line vs. the right line.
Performing a linear fit to x and y using np.polyfit (function draw_line()).
Then using the coefficients of the fit to average the position of each of the lines and extrapolate to the top and bottom of the lane. Finally draws it on the image `img` using `color` and `thickness` for the line.


## 2. Identify potential shortcomings with your current pipeline

- The lines shake too much on the videos
- The line size is not optimal


## 3. Suggest possible improvements to your pipeline

- Improve the line extrapolation to reduce the line shaking
