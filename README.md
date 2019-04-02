# **Finding Lane Lines on the Road** 

Vinh Nghiem

Self-Driving Car Engineer Nanodegree Program

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project lane lines in video frames are detected using a pipeline of Gaussian filtering, Canny edge detection, and Hough Line Transforms. Python and OpenCV is used.  


Running the project
---

**Step 1:** Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7) if you haven't already.

**Step 2:** Open the code in a Jupyter Notebook

All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, use terminal to navigate to your project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) installation instructions!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  

Reflections
---
**1. Pipeline**

1- Converted the original color image with 3 channels to grayscale image with 1 channel

2- Converted grayscale image to Gaussian filtered image to smooth out noise

3- Converted Gaussian filtered image to image with edges using Canny edge detection

4- Converted image with Canny edges to image with edges only in region of interest on black background :

a. Defined mask (numpy array) with same dimensions as Canny image, with black background

b. Apply bitwise-and operation to Canny image and mask 

5 – Found lines in Canny edged image using Hough Transform, stored as numpy array 

6 – Drew Hough lines on image with black background:

a. Defined mask (numpy array) with same dimensions as original image (with 3 channels), with black background

b. Drew lines on mask 

7 – Performed weighted addition operation on original image array and array representing Hough lines on image with black background 

8 – Returned resulting image array

**2. Potential Shortcomings**
If there are any objects in the same lane, such as tree branches, lumber, rain, snow, trash, road imperfections, shadows, hanging tree branches, animals, passing motorcycles, these will be interpreted as lines that will incorrectly influence the lane line determination.

**3. Possible Improvements to pipeline**
The potential shortcoming, of objects in the lane, has already been partly addressed in the current pipeline by:

Only accepting candidate lines of a certain pixel length (a parameter in the Hough Line Transform), and also only accepting lines of at least a certain slope. This is able to select out the dashboard in the challenge video, and a large number of road imperfections and shadows.

A big possible improvement would be to recognize other possible objects in the lane, using machine learning, so that the objects are not considered in the lane line calculations.
