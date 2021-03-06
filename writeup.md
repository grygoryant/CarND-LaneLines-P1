# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[initial]: ./writeup_images/initial.png "Initial image"
[h_channel]: ./writeup_images/h_channel.png "H channel image"
[l_channel]: ./writeup_images/l_channel.png "L channel image"
[s_channel]: ./writeup_images/s_channel.png "S channel image"
[white_areas]: ./writeup_images/white_areas.png "White areas image"
[yellow_areas]: ./writeup_images/yellow_areas.png "Yellow areas image"
[color_mask]: ./writeup_images/color_mask.png "Color mask image"
[masked_image]: ./writeup_images/masked_image.png "Masked image"
[blurred]: ./writeup_images/blurred.png "Blurred image"
[edges]: ./writeup_images/edges.png "Edges image"
[roi]: ./writeup_images/roi.png "ROI image"
[result]: ./writeup_images/Result.png "Result image"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 8 steps.

![alt text][initial]

1. Converting image from RGB to HLS color scheme. 

I decided to choose HLS color scheme because white and yellow colors are clearly expressed in separate channels of this color model.
Here's the examples of splitting image to three channels:

![alt text][h_channel]
![alt text][l_channel]
![alt text][s_channel]

As we can see, white color is well distinguishable in the L channel, while yellow in the S channel.

2. Color thresholding.

In this step we use splitted HLS channels to extract white color areas and yellow color areas. In order to do this we use thresholding operation.

![alt text][white_areas]
![alt text][yellow_areas]

After that we combine those two results to get color mask.

![alt text][color_mask]

3. Masking image with color mask.

Here we apply the mask from the previous step to get all neccessary zones on a picture.

![alt text][masked_image]

4. Blurring masked image.

In order to avoid noises, we apply gaussian blur filter on the masked image.

![alt text][blurred]

5. Canny edge detector.

Now our image has nice contrast, so we can apply edge detector.

![alt text][edges]

6. Mask image using ROI mask.

In order to select only that area of picture, that is interesting for us, we applying perspective ROI mask.

![alt text][roi]

7. Hough transform.

Detected edges allow us to use Hough transform to get all straight lines from our image.

8. Finally, we extrapolate and get avaraged road lanes.

It is neccessary to say, how extrapolating and averaging works.

Step #7 gives us a set of points, which are the ends of lines. We select the medium point and checks, if given line point lies on the right or on the left side of that middle point. If one of the two line points lies on the left side of middle point, then this line is the left line. The same logic is used to find all segments of the right line.

As for averaging, we simply store the deque of several previous values of line coefficients and on each iteration we just count the average value of that coefficients.

And here's the final result:

![alt text][result]

I made draw_lines() the member function of my SimpleLaneDetector in order to use members of SimpleLaneDetector class.

### 2. Identify potential shortcomings with your current pipeline

I think, that this approach depends a lot on the brightness of given picture and the lighting of scene. 
So it could be dificult to detect lanes in shadowy areas, at night etc.

Also it could be dificult to solve cases, when, for example, white car is taken for the road lane.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use another method of selecting segments of right and left lanes, based on the slope angle of segments.