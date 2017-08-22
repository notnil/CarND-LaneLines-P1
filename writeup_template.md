# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following steps:
- blur the image with a gaussian blur
- transform the image to only edges using canny transform
- black out pixels not in region of interest
- detect line segments within the region of interest
- split lines into two sections: left and right lane divider 
For each bucket:
- find the longest line
- calculate slope and y-intercept
- reform line within region of interest
draw on copy of the original image

I used the draw_lines() function in its original form and just passed in lines that I calculated.   

### 2. Identify potential shortcomings with your current pipeline

There are shortcomings on relying on the longest line to represent the entire lane divider.  The hough line produced lots of little lines instead of all encompassing larger ones.  The largest within a lane divider group might differ significantly from the orientation of the trend line.  This method also produced zero slope lines for a few frames in the video which required special handling.

### 3. Suggest possible improvements to your pipeline

The implementation could be improved by computing a weighted average of y-intercept and slope values based on line distance.  Instead of wholly relying on the longest line for its y-intercept and slope, each detected line would influence the output in proportion to its length.  This change would result in a more accurate portrayal of the overall trend line for each lane divider.