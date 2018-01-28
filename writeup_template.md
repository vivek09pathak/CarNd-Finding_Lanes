# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Pipeline Description:
   * **My pipeline consisted of 7 steps.**
     *  **Step 1:** Converting my image to Gray-Scale.
     *  **Step 2:** Applying Gaussian blur to Gray-Scale image for further smoothening and suppressing noise and eliminating spurious                        gradients by averaging and save image output in the blur.
     *  **Step 3:** On Gaussian smoothen image called blur we apply canny edge detection to detect edges on the image by setting                             threshold.
     *  **Step 4**  Now, masking image with region_of_interest function on canny image(edge).I have taken a quadrilateral polygon as                         region of interest.
     *  **Step 5**  Apply hough transform on region of interest image(mask) to get lane lines on the road.
     *  **Step 6**  Extrapolating on lines detcted from hough transform to draw continous lines on the image.
     *  **Step 7**  Image obtained from Extrapolating we apply it with initial image to get final image as result.
   * **In order to draw a single line on the left and right lanes, I modified the draw_lines() function as follows:**
   
		* From the draw_lines function I have called the extrapolating_lines() function with lines obtained from hough transform and masked image on which lines has to been drawn.In function I have appended the left and right coordinates	in array by taking midpoint of the image and slope < 0.2 to segregate left lane otherwise as right lane.For non empty array passed array of x and y coordinates in polyfit function to get slope and coefficient of gradient for the lanes.Then, passed the masked image,polyfit values and array of x,y values to respective right and left lane function to draw lines.To draw lines,Taken min and max value from the array for x coordinates and put those value in Y=mX+c function to get y-coordinates and drawn lines using cv.line() function.	 
		* For the bad frames where vector return empty array I have taken a global variable to take previous frame values and passed values as described above to draw lines for contionus lanes lines.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
