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

## Code analysis

### Lucas Kanade

- The points we get from corner detection are going to be tracked
- The window size has a tradeoff with noise. Smaller windows are more sensitive to noise but can miss out on larger motions
- Uses Level2 of the image pyramid ie. 1/4th the resolution of the image
- Criteria is the max number of iterations and the epsilon value shows the tradeoff between speed and accuracy of tracking
- The mask is just to visuaize the points
- The calcOpticalFlowPyrLK method calculates the next points on the basis of current, previous image and previous points.
- It also returns the status array which has a value 1 for the point for which flow has been found
