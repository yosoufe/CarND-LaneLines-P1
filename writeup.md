#**Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./output_test_images/img_gray "Grayscale"

[image2]: ./output_test_images/blur_img "Blured"

[image3]: ./output_test_images/edges "Edges"

[image4]: ./output_test_images/img_ROI "Grayscale"

[image5]: ./output_test_images/hough_output "Lines"

[image6]: ./output_test_images/Extended_averaged_line "Extended Averaged Lines"

[image7]: ./output_test_images/final_img "Result"


---

### Reflection

###1. The Pipeline:

* The color image is transformed to a grayscale one.

![alt text][image1]

* The Gaussian filter is applied on the grayed scale image.

![alt text][image2]

* The Canny edge detection algorithm is applied to the ROI.

![alt text][image3]

* A region of interest (ROI) is designed to capture in front of the car.

![alt text][image4]

* The Hough algorithm applied to the binary image at the output of the edge detection. The output is the line equations in image space.

![alt text][image5]

* based on the slope of the equation, the lines are chosen. The ones with the slope between -1 and -2 considered as left line, the ones with the slope between 1 and 2 labelled as right lines. The rest are ignored.
* The left and right lines are averaged. It means the final unique left line is the line with the slope and bias, averaged over all left line and the same for the roght line.
* The lines are drawn in the ROI. This can also be called as extrapolation.

![alt text][image6]

* All the parameters of the algorithm were chosen roughly until this step. Now the parameters tuned firstly for sample images to get a proper output over all of them.
* A weighted sum of the source image and the line image is returned as the output of `process_image` function.

![alt text][image7]

* The parameters are retuned for the first video and then second video.


###2. Identify potential shortcomings with your current pipeline


0. The program can only handle few situations. That means these codes are designed only for two given straight video in highways. There are many different situations exists which this code probably cannot detect the lane.
0. The system is only looking at a specific ROI which may always not keeping useful information about environment.

0. It is assumed that the lines are straight which is not always correct

0. The detected lines are vibrating especially when there is a long gap between real lanelines.


###3. Suggest possible improvements to your pipeline
0. Algorithm can be tested over a lot of videos while it can be bothersome.
0. If it would be possible to add information of previous frames to solve for the current, there would be a lot of  possible solutions for the problems above like:
	0. Choosing the ROI based on the previous frame. For example the new ROI in current frame could be the position of the previous detected line, but only a bit bigger (based on the speed and heading information). This also avoid the noises and decreases the calculation cost.
	0. Averaging lines over sequence of frames could attenuate the vibration.
0. Using higher order curves instead of straight lines, can also reduces the vibration and better detection.
