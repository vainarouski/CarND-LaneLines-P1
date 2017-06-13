# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve_gray.jpg "Grayscale"
[image2]: ./test_images_output/solidWhiteCurve_blur.jpg "Gaussian smoothing"
[image3]: ./test_images_output/solidWhiteCurve_edges.jpg "Canny edge detection"
[image4]: ./test_images_output/solidWhiteCurve_masked.jpg "Selected area of interest"
[image5]: ./test_images_output/solidWhiteCurve_lines.jpg  "Hough transform"
[image6]: ./test_images_output/solidWhiteCurve_result.jpg  "Hough transform"



---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:

#### 1. Converted the images to grayscale:

![alt text][image1]

#### 2. Applied Gaussian smoothing and Canny edge detection:

![alt text][image2]

![alt text][image3]

#### 3. Removed all unnecessary from the image and left only the part of the road that interests me:

![alt text][image4]

#### 4. Applied Hough transform:

![alt text][image5]

#### 5. Combined the resulting image after Hough transform with the original image:

![alt text][image6]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function. First, to remove a 
noise, I calculated slope for every line: ```slope = (y2-y1)/(x2-x1)``` and found approximate range for left and right 
line slope: ```0.55 > slope < 0.85```, so it helped me to remove all, for example, vertical and horizontal lines from 
image. Next, I divided all the coordinates of the lines into two groups, if slope positive I added it to the left line 
group, if negative to the right line group. Next, using coordinates values I built a linear regression model for right 
and left lines. From linear model I found slope and intercept for left and right lines, and based on these values I 
calculated coordinates for points: ```y1 = img.shape[0]``` and ```y2 = min(left_y)```. Next, I just draw the lines based 
on these coordinates.

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be a lot of lines on the road, for example, bad road surface with a lot of cracks. It 
will be hard to correctly identify lines on the road (a lot of noise).
Another shortcoming could be different zoom level of the camera. Since I used very narrow area of the road to identify 
lines. If zoom level will be bigger, lines can go out of the recognized area.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use some filters to reduce the noise.

Another potential improvement could be some algorithm which will identify image zoom level. 
