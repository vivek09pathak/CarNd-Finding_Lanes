# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurve"
[image2]: ./test_images_output/solidWhiteRight.jpg  "solidWhiteRight"
[image3]: ./test_images_output/solidYellowCurve.jpg "solidYellowCurve"
[image4]: ./test_images_output/solidYellowCurve2.jpg "solidYellowCurve2"
[image5]: ./test_images_output/solidYellowLeft.jpg "solidYellowLeft"
[image6]: ./test_images_output/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch"

---

### Reflection

### 1. Pipeline Description:
   * **My pipeline consisted of 7 steps.**
     *  **Step 1:** Converting my image to Gray-Scale.
     *  **Step 2:** Applying Gaussian blur to Gray-Scale image for further smoothening and suppressing noise and eliminating spurious                       gradients by averaging and save image output in the blur.
     *  **Step 3:** On Gaussian smoothen image called blur we apply canny edge detection to detect edges on the image by setting                             Low and high threshold as 50 and 150 respectively.
     *  **Step 4**  Now, masking image with region_of_interest function on canny image(edge).I have taken a quadrilateral polygon as                         region of interest and have taken differents ROI for Videos.As for **solidWhiteRight** (0,imshape[0]),(410,340), (590,340),(imshape[1],imshape[0]) and for **solidYellowLeft** (0,imshape[0]),(410,360), (590,360),(imshape[1],imshape[0])
     *  **Step 5**  Apply hough transform on region of interest image(mask) to get lane lines on the road.
     *  **Step 6**  In extrapolating on lines detcted from hough transform to draw continous lines on the image from hough transform function I have called separate_lines.
     *  **Step 7**  Image obtained from separate_lines() we apply it with initial image to weighted_img function to get final image as result.
   * **In order to draw a single line on the left and right lanes, I modified the draw_lines() function as follows:**
   
		* From the draw_lines function I have called the separate_lines() function with lines obtained from hough transform and masked image on which lines has to been drawn.In function I have appended the left and right coordinates in array by taking x2 < 500 and x1<480 value of the image and slope < 0.2 to segregate left lane otherwise as right lane.For non empty array passed array of x and y coordinates in polyfit function to get slope and coefficient of gradient for the lanes.Then, passed the masked image,polyfit values and array of x,y values to respective right and left lane function to draw lines.To draw lines,Taken min and max value from the array for x coordinates and put those value in Y=mX+c function to get y-coordinates and drawn lines using cv.line() function.	 
		* For the bad frames where vector return empty array I have taken a global variable to take previous frame values and passed values as described above to draw lines for contionus lanes lines.

Below are the output of an image: 

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]


### 2. Identify potential shortcomings with your current pipeline
   * One potential shortcoming would be that taking in consideration of previous frame to draw lines in-case of no lines detected 
   * Secondly,the pipeline will not able to detect different intesity of same color on the lane.


### 3. Suggest possible improvements to your pipeline
   * A possible improvement would be that building method to able to generate different region of interest for different situations.
   * Using different models to detect color of lines of different intensity for same color due to shadow,etc so that lane can be indentified correctly.
