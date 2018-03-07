#### For Line curvatures

==>> canny use of sobel vs sobel

Sobel Use
1. Apply sobel 
  sobelx = cv2.Sobel(gray, cv2.CV_64F, 1, 0)
  Calculate the derivative in the yy direction (the 0, 1 at the end denotes yy direction):
  sobely = cv2.Sobel(gray, cv2.CV_64F, 0, 1)
  output datatype is cv2.CV_8U or np.uint8. But there is a slight problem with that. Black-to-White transition is taken as Positive slope   (it has a positive value) while White-to-Black transition is taken as a Negative slope (It has negative value). So when you convert data   to np.uint8, all negative slopes are made zero. In simple words, you miss that edge.
  Solution : cv2.CV_16S, cv2.CV_64F
  Since we are searching for the gradient around a given pixel, we want to have an equal number of pixels in each direction of the region   from this central pixel, leading to an odd-numbered filter size - a filter of size 
  ex : sobely = cv2.Sobel(gray, cv2.CV_64F ,0,1,ksize = 7)
  magnitude and scalling :  gradmag = np.sqrt(sobelx**2 + sobely**2)  scaled_sobel = np.uint8(255*gradmag/np.max(gradmag))
  direction : np.arctan2(sobely/sobely)
  
1. camera clibratting--> generate coficient
2. undistort image 
3. thresholding -->> x - grad, y - grad, mag grad, directional grad find lane line --->>. binary image
4. Color space changing --> chooseing color channels for finding lane line--- binary image
5. combile 4 and 5 binary image
6. percpective transformation
7. detect lanes lines -- > ay2 + by + c
8. calculate curvature
