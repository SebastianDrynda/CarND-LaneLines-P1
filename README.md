# Udacity Self-Driving Car Nanodegree - Project Finding Lane Lines on the Road

This Git repository contains the code written to complete the first project on Udacity Self-Driving Car Nanodegree. This project consists of algorithms to identify lane lines on the road on a video. The video is taken from a camera at the center of a vehicle.

## Prerequisites

To run this project, you need [Anaconda](https://anaconda.org/) or [Miniconda](https://conda.io/miniconda.html) installed (please visit [this link](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) for more information.)    
Here is a great link for learning more about [Anaconda and Jupyter Notebooks](https://classroom.udacity.com/courses/ud1111).

## Installation
To create an environment for this project use the following command:

```
conda env create -f environment.yml
```

After the environment is created, it needs to be activated with the command:

```
source activate carnd-term1
```
and open the project's notebook [P1.ipynb](P1.ipynb) inside jupyter notebook:

```
jupyter notebook P1.ipynb
```

## Overview

The repository contains the jupyter notebook [P1.ipynb](P1.ipynb) where the processing image pipeline is implemented.    
The image pipeline consists on 6 steps:   

**Image Pipeline step 1: Converting images into gray scale**    
def image_pipeline_gray(image)    
Returns a gray scaled version of the input image using cv2.cvtColor method. 

**Image Pipeline step 2: Applying Gaussian smoothing**    
def image_pipeline_gaussian_blur(image)    
Applies a Gaussian blur to the provided image using cv2.GaussianBlur method    
 
**Image Pipeline step 3: Applying Canny transform**    
def image_pipeline_canny(image)    
Use a Canny transformation to find edges on the image using cv2.Canny method.
 
**Image Pipeline step 4: Applying Region of Interest**    
def image_pipeline_roi(image)    
Masks the image segments that are not interesting in regards to the line detection.

**Image Pipeline step 5: Applying Hough transform**    
def image_pipeline_hough(image)    
Use the Hough transformation to find the lines on the masked image using cv2.cv2.HoughLinesP. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 
separating line segments by their slope to decide which segments are part of the left line vs. the right line.
Performing a linear fit to x and y using np.polyfit. Then, using coefficients of the fit to average the position of each of the lines and extrapolate to the top and bottom of the lane.  For removing lane shakiness, the average of the current frame lines and the previous frame lines (only x1 and x2) is computed. If the difference between x and x_prior is higher than a tolerance value, the x_prior value is taken. Finally draws it on the image `img` using `color` and `thickness` for the line.

**Image Pipeline step 6: Merging original image with Hough transform lines**   
def weighted_img(image)    
Merges the output of hough transformation with the original image to represent the lines on it. 



First, the pipeline is tested agains the images contained at [test_images](test_images). The output of each step is saved in a directory:

- [test_images_gray](test_images_gray)
- [test_images_gaussian_blur](test_images_gaussian_blur)
- [test_images_canny](test_images_canny)
- [test_images_roi](test_images_roi)
- [test_images_hough](test_images_hough)
- [test_images_merged](test_images_merged)

After that test, the pipeline is consolidated on a single function **process_image** to apply it on a video frame. The sample videos could be found [here](test_videos).
The video after the transformation are saved on the [test_videos_output][test_videos_output] directory.


## License
This project copyright is under [MIT](LICENSE) License.
