# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

![image1](/test_images_output/solidWhiteRight.jpg "Example output")
![image2](/test_images_output/solidYellowCurve2.jpg "Example output 2")

### Reflection

My pipeline is located in the `detect_lane_lines()` function. It consists out of 6 steps. We'll walk through the 
pipeline with the following example image.

![start](/test_images/solidWhiteRight.jpg "Start")

1. Converting an image to Grayscale
Uses the `cv2.cvtColor` function for transforming the incoming image to a grayscale format. 

![grayScale](/test_images/solidWhiteGray.jpg?raw=true "Grayscale" )

2. Apply an extra Gaussian Blur
The Canny Edge detection also applies a Gaussian Blur but we apply one extra for better results. In this case
we apply one with a `kernel size` of `3`

![blurred](/test_images/solidWhiteBlurred.jpg "Blurred" )

3. Execute Canny Edge detection on the image
In this case I've chosen to go with a `low_threshold` of `50` and a `high_threshold` of `150`. This respects the `1:3` ratio that's recommended by Canny himself.

![canny](/test_images/solidWhiteCanny.jpg "Canny")

4. Add a mask
We only want to look for lines in a certain region. This is why we apply a mask to the original Canny Edge image. For this exercise i've defined the mask as:
`[[(0, image.shape[0]), (0.45 * image.shape[1], 0.58 * image.shape[0]), (0.55 * image.shape[1], 0.58 * image.shape[0]), (image.shape[1], image.shape[0])]]`

![mask](/test_images/solidWhiteRegion.jpg "Region")

5. Calculate lines
Using the HoughLinesP algorithm we calculate the lines. For the `rho` value I've chosen `3`, `theta` equals `pi/180`, the `threshold` is `150`, `min_line_len` equals `30` and the `max_line_gap` is `100`.

![lines](./test_images/solidWhiteLines.jpg "Lines")

6. Merge lines with original image
Last up we merge the original image with the calculated lines using the `weighted_img()` function.

![final](/test_images_output/solidWhiteRight.jpg "Final")
