Download Link: https://assignmentchef.com/product/solved-computer-vision-i-project-2
<br>
<span style="font-size: 2.61792em; letter-spacing: -1px; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;">Image Mosaicing</span>

The purpose of this project is to find corner features in multiple images and to align the images in a mosaic by estimating a homography between corresponding features.

<ol>

 <li><strong>Overview:</strong></li>

</ol>

In this project you will apply a Harris corner detector to find corners in two images, automatically find corresponding features, estimate a homography between the two images, and warp one image into the coordinate system of the second one to produce a mosaic containing the union of all pixels in the two images.

<ol start="2">

 <li><strong>Project Requirements:</strong></li>

</ol>

(a) Write a program to implement the above ideas. Sample images to test your program will be available in blackboard. The basic outline of your program should be as follows:

<ol>

 <li>Read in two images. (Note: if the images are large, you may want to reduce theirsize to keep running time reasonable! Document in your report the scale factor you used.)</li>

 <li>Apply Harris corner detector to both images: compute Harris R function over theimage, and then do non-maimum suppression to get a <strong>sparse set </strong>of corner features. iii. Find correspondences between the two images: given two set of corners from the two images, compute normalized cross correlation (NCC) of image patches centered at each corner. (Note that this will be O(<em>n</em><sup>2</sup>) process.) Choose potential corner matches by finding pair of corners (one from each image) such that they have the highest NCC value. You may also set a threshold to keep only matches that have a large NCC score.</li>

 <li>Estimate the homography using the above correspondences. Note that these cor-respondences are likely to have many errors (outliers). That is ok: you should use RANSAC to robustly estimate the homography from the noisy correspondences:

  <ol>

   <li>Repeatedly sample minimal number of points needed to estimate a homography(4 pts in this case).</li>

   <li>Compute a homography from these four points.</li>

   <li>Map all points using the homagraphy and comparing distances between pre-dicted and observed locations to determine the number of inliers.</li>

   <li>At the end, compute a least-squares homgraphy from <strong>ALL </strong>the inliers in the largest set of inliers.</li>

  </ol></li>

 <li>Warp one image onto the other one, blending overlapping pixels together to createa single image that shows the union of all pixels from both input images. You can choose which of the images to warp. The steps are as follows:

  <ol>

   <li>Determine how big to make the final output image so that it contains the unionof all pixels in the two images.</li>

   <li>Copy the image that does not have to be warped into the appropriate locationin the output.</li>

   <li>Warp the other image into the output image based on the estimated homography(or its inverse). You can use matlab functions if you want or write your own warping function.</li>

   <li>Use any of the blending schemes we will discuss in class to blend pixels in thearea of overlap between both images. (b) <strong>Write a report. </strong>The report should include:</li>

  </ol></li>

 <li>Abstract, description of algorithms, experiments, values of parameters used, obser-vations and conclusions.</li>

 <li>A FLOWCHART, input and output images.</li>

</ol>

<ul>

 <li>An image showing potential corner feature location matches between the two images.An example of how to show them is given in the figure below. iv. An appendix with your source code</li>

</ul>

<strong>Extra Credit </strong>Warp one image into a “frame” region in the second image. To do this, let the points from the one view be the corners of the image you want to insert in the frame and let the corresponding points in the second view be the clicked points of the frame (rectangle) into which the first image should be warped (Look at Matlab’s ginput function for an easy way to collect mouse clicks). Use this idea to replace one surface in an image with a picture of your pet or project a drawing from one image onto the street in another image, or paste a powerpoint slide on a movie screen, etc … Be creative! Send me your result by email so I can share it with the rest of the class.

2

(a)                                                                                                           (b)

(c)

3

Figure 1: (a) Corresponding matches with outliers; (b) after they are cleaned and (c) the final mosaic