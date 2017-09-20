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

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 8 steps.
1. Converting image from RGB to HLS color scheme. 

I decided to choose HLS color scheme because white and yellow colors are clearly expressed in separate channels of this color model.
Here's the examples of splitting image to three channels:

![alt text][h_channel][l_channel][s_channel]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][initial]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
