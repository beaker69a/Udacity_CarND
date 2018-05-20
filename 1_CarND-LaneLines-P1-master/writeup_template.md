# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

In this project I will take photos and movies and find and drawe lane lines.
I will create a pipeline that will do the following.
  To find the lane lines I will use following techniques:
     * Color Selection
     * Canny Edge Detection
     * Region of Interest Selection
     * Hough Transform Line Detection 
     
Then I will put it all togeather to draw the lane lines on the output images.
I will the use the same techniques to draw on video files.


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline uses many steps to detect and mark the lines.
  The first step I convert the image to HSL and return an image with just the white and yellows.

Then I convert image to grayscale.
   This measures the magnitude of pixel intensity changes or gradients​, making it easer to detect.
   

Then I blur the image with kernel size of 3.
   This make the edges smoother.

Then I use canny edge detection.
   Using low thershold of 50 and high threshold of 150 seamss to detect the edges of the lane lines well.

The next step I used is to get the image shape.
   I can then use row and column for my lest and right lane lines.
   I put this into a vertices array.
   
I can now set my region of interest
   Usint the vertices array, I can now set the area of the image that I want to detect (only the lane lines).
   
I am now ready to detect lines in the edge images.
  Using hough_lines function I can detect the edges. 
  I am using rho of 2. This is the distance resolution.
  For the theta I am using np.pi/180 for the angle resolution.
  The threshold I have set at 50. This only those lines are returned that get enough votes.
  For the minLineLength I am using 10. This will be my minimum line length.
  For maxLineGap I will use 20. This is my maximum allowed gap between points on the same line to link them.

  Now I can adverage the slopes to set the lines length and size.
  Now that I have the lines detected I can draw them on the iamge.

Now it time to combine the images.
  Using cv2.addWeighted I am combining the image I have been working on with the test image.
  This draws the lines on the test image.

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

Lane lines I have made are the same color.
  I was not sure if I needed to mark the yellow lines with yellow marks and the white lines with white marks.

My pipeline only detects the straight lane lines. 
  The roads have curves, therefor my lines jump around when there is a curve as it is looking for streight lines.

I have used a conversion to HSL so I can detect the lane line better.
  The dark lines due to shadow, rain, low light are hard to detect. HSL seams to be working for this project.
  
 
### 3. Suggest possible improvements to your pipeline

I could detect corners better. This my make my lines not dance so much.
Mark the yellow lane line with a yellow mark
Mark the white lane line witha white mark.

