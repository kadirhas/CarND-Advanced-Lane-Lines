## Advanced Lane Finding

In this project, a robust lane detection algorithm which can also provide curvature of the road and the lateral position of the vehicle with respect to the center of the lane has been developed. In the following section, all of the criterias will be addressed. Brief explanation of how the code is working will also be provided.


[//]: # (Image References)

[image1]: ./output_images/chessboard_calibration.png "Chessboard calibration"
[image2]: ./output_images/undistort.png "Undistorting the image"
[image3]: ./output_images/undistort.png "Undistorting the image"
[image4]: ./output_images/undistort.png "Undistorting the image"
[image5]: ./output_images/undistort.png "Undistorting the image"
[image6]: ./output_images/undistort.png "Undistorting the image"
[image7]: ./output_images/undistort.png "Undistorting the image"

The Project Rubric
---
# Readme
#### The writeup / README should include a statement and supporting figures / images that explain how each rubric item was addressed, and specifically where in the code each step was handled.
This document is provided for this purpose

# Camera Calibration
#### Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.
The provided chessboard pictures first converted to grayscale. Then with the opencv function each corner of the chessboard is found. 
![alt text][image1]
Since the distance of the each corner of a chessboard should be equal, the image is adjusted with this information via opencv function.


# Pipeline (test images)
#### Provide an example of a distortion-corrected image.
The following image shows clearly the effect of distortion correction.
![alt text][image2]
#### Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image. Provide an example of a binary image result.
The common points of sobelx and sobely is combined since the lanes can appear on both of them clearly. With taking only common points, some of the distortion is removed. The same idea is used for magnitude and direction of the gradients. Since the lanes are expected in a certain angle, this information is utilized. However this information alone is too noisy. To remove it, the magnitude of the each gradient is also thresholded and only common points are used. On some sections of the road, color is really helpful since it doesn't affect from shadows etc. Because of this, HLS and Lab colorspaces is used to get the lines. 
The three combined images are also combined to add up all information from each combination. The results can be seen under output_images folder or in the LaneFinder.ipynb
#### Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.
On one of the corrected images with straight lanes, four points on the lanes are chosen. They are ([574,466],[710,466],[1069,701],[232,701]). Then, another four points are chosen to create a shape of a rectangle. These settings can be found in the function called as warpSettings. 


