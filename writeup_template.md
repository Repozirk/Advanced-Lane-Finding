
**Advanced Lane Finding Project**

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image1]: ./output_images/corners/corners_calibration3.jpg "Detect Chessboard Corners"
[image2]: ./output_images/undistorted/undist_calibration3.jpg
[image3]: ./output_images/undistorted/undist_test6.jpg 
[image4]: ./output_images/undistorted/undist_test3.jpg
[image5]: ./output_images/pipeline/comb_test3.jpg
[image6]: ./output_images/warped/perspective_undist_straight_lines1.jpg
[image7]: ./output_images/warped/perspective_undist_straight_lines2.jpg
[image8]: ./output_images/warped/warped_test3.jpg
[image9]: ./output_images/find_lanes/sliding_window.png
[image10]: ./output_images/find_lanes/ploynominal.png
[image11]: ./output_images/find_lanes/unwarped_with_data.png

[video1]: ./output_video.mp4 "Video"

## [Rubric](https://review.udacity.com/#!/rubrics/571/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

### Camera Calibration


#### 1. Computation of camera matrix and distortion coefficients.

The code for this step is contained in the third code cell of the IPython notebook.

The "object points" are the x and y values, assuming the chessboard is fixed on the (x, y) plane at z=0. Thus, objp is just a replicated array of coordinates, and objpoints will be appended with a copy of it every time I successfully detect all chessboard corners in a test image. Imgpoints will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.

By use of `cal_undistort` in the second code cell of the IPython notebook, the camera calibration and distortion coefficients are computed
I then used the output objpoints and imgpoints to compute the camera calibration and distortion coefficients using the cv2.calibrateCamera() function. Applying this distortion correction to the test image using the cv2.undistort() function and obtained this result:

![alt text][image1] ![alt text][image2]



### Pipeline (Test images)


#### 1. Example of a distortion-corrected image.

Applyingh teh undistortion function will deliver following result:

![alt text][image3]


#### 2. Ceate a thresholded binary image.  Example of a binary image result.

I used a combination of color thresholds (hls and hsv) and gradient thresholds to generate a binary image (function for color threshold `color_threshold()` and gradient threshold `abs_sobel_thresh()` are located in the second code cell of the IPython notebook, Applying these functions can be seen from  code cell 5 from line #28). Here is the test_image_3 and binary_image_3:

![alt text][image4] ![alt text][image5]


#### 3. Performing perspective transform. Example of a transformed image.

The code for the perspective transform includes a function called `warper()`  The `warper()` function is applied in code cell 5 line #52 and takes as inputs an image (`img`), source (`src`) and destination (`dst`) points.  These are the chossen source and destination points 

```python
    src=np.float32([[753,480],
                    [537,480],
                    [190,700],
                    [1150,700]])

    
    dst=np.float32([[1140,100],
                    [200,100],
                    [200,740],
                    [1140,740]])
```


The verification of the perspective transform was achieved by running this function on the straight line test images. 

![alt text][image6] ![alt text][image7] 


#### 4. Identification of lane-line pixels and fit their positions with a polynomial.

Here the suggestion of the Udacity solution was applied (see code cell 5 from line #73) and delivered following outputs:

![alt text][image8]
![alt text][image9]
![alt text][image10]


#### 5. Calculation of the radius of curvature of the lane and the position of the vehicle with respect to center.

I did this in lines # through # in my code in `my_other_file.py`

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in lines # through # in my code in `yet_another_file.py` in the function `map_lane()`.  Here is an example of my result on a test image:

![alt text][image6]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
