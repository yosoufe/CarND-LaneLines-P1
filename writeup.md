#**Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./output_test_images/img_gray.jpg "Grayscale"
[image2]: ./output_test_images/blur_img.jpg "Blured"
[image3]: ./output_test_images/edges.jpg "Edges"
[image4]: ./output_test_images/img_ROI.jpg "Grayscale"
[image5]: ./output_test_images/hough_output.jpg "Lines"
[image6]: ./output_test_images/Extended_averaged_line.jpg "Grayscale"
[image7]: ./output_test_images/final_img.jpg "Result"


---

### Reflection

###1. The Pipeline:

1. The color image is transformed to a grayscale one.

![alt text][image1]

2. The Gaussian filter is applied on the grayed scale image.

![alt text][image2]

3. The Canny edge detection algorithm is appled to the ROI.

![alt text][image3]

4. A region of interest (ROI) is designed to capture in front of the car.

![alt text][image4]

5. The Hough algorithm applied to the binary image at the output of the edge detection. The output is the line equations in image space.

![alt text][image5]

6. based on the slope of the equation, the lines are chosen. The ones with the slope between -1 and -2 considered as left line, the ones with the slope between 1 and 2 labelled as right lines. The rest are ignored.
7. The left and right lines are averaged. It means the final unique left line is the line with the slope and bias, averaged over all left line and the same for the roght line.
8. The lines are drawn in the ROI. This can also be called as extrapolation.

![alt text][image6]

9. All the parameters of the algorithm were chosen roughly until this step. Now the parameters tuned firstly for sample images to get a proper output over all of them.
10. A wighted sum of the source image and the line image is returned as the output of `process_image` function.

![alt text][image7]

11. The parameters are retuned for the first video and then second video.


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
