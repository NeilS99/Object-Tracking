# Object Tracking

## Notes

### 1) Optical Flow

- Optical flow is the pattern of apparent motin of image objects between two consecutive frames caused by the movement of an object or camera
- Assumes neighboring pixels have a similar motion and instensities of the object don't change
- In OpenCV, the optical flow method takes in a bunch of points and then tracks those points in the next frame.
- It uses the lucas-kanade function in which we pass the prev frame, prev points and current frame
- The lucas-kanade function computes optical flow for a sparse feature set. This means only for the points it was told about not all the points in a video
- For this we use Gunner Farneback's algorithm to calculate dense optical flow
- It will calculate the flow for all points and color them black if no flow is detected

### 2) Meanshift and Camshift Tracking

- In the general meanshift algorithm, for a set of points, the direction to the closest cluster centroid is determinded.
- After a few iterations, the algorithm finds a number of clusters where all points have shifted and converged.
- Meanshift can be given a target to track, calculate the color histogram of the target area, and then keep sliding the tracking window to the closest center
- Just using meanshift won't change the window size if the target moves away or towards the camera. Thus, here we use CAMshift to update the window size.
