

[//]: # (Image References)

[image1]: ./output_images/image1.PNG
[image2]: ./output_images/image2.PNG
[image3]: ./output_images/image3.PNG
[image4]: ./output_images/image4.PNG
[image5]: ./output_images/image5.PNG
[image6]: ./output_images/image6.PNG
[image7]: ./output_images/image7.PNG
[video1]: ./project_video_out.mp4



### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

I used `cv2.findChessboardCorners` to find chessboard corners in the images, and created standard chessboard object points by `objp[:,:2] = np.mgrid[0:9,0:6].T.reshape(-1,2)`. Then I used `cv2.calibrateCamera` to find camera matrix and distortion coefficients. Finally I used `cv2.undistort` to apply undistortion to original image.

![alt text][image1]

### Pipeline (multiple images)

#### 1. Provide an example of a distortion-corrected image.

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:
![alt text][image2]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I used a combination of color and gradient thresholds to generate a binary image.

![alt text][image4]
![alt text][image5]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

I used 4 fixed points as source and middle part of image as destination. Then apply `cv2.getPerspectiveTransform` and `cv2.warpPerspective` to get warped image.

```python
src = np.float32([(600,450),
                  (700,450), 
                  (300,650), 
                  (1000,650)])
dst = np.float32([(450,0),
                  (width-450,0),
                  (450,height),
                  (width-450,height)])
```

This resulted in the following source and destination points:

| Source        | Destination   | 
|:-------------:|:-------------:| 
| 600, 450      | 450, 0        | 
| 700, 450      | 830, 0      |
| 300, 650     | 450, 720      |
| 1000, 650      | 830, 720        |


![alt text][image3]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

I used the sliding windows search introduced in lecture, result looks like

![alt text][image6]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

I used my function curv_and_dist() to find the curvature and distance from center

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.


![alt text][image7]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video_out.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  
