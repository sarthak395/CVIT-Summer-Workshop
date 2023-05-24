# Document Imaging

# Task 1 - Skew Detection and Correction
Detecting skew in the image (angle with which it is rotated) and further correct it to get the correct orientation

## Canny filters - Blurring + EdgeDetection
## Hough transforms - Detecting shapes
- Hough accumulator : Number of points through which a line passes
- Non-maximum suppression : Filtering out non-relevant lines
## Detecting dominant angle
- to get the orientation/skew angle , we have to subtract by 90
## Rotating
- Affine Transformation 




# Task 2 - Word Detection Contours
Detecting words in an image and drawing contours around it

## Denoising the image
## Text dilation - to enlarge each letter and remove gaps inside words
## Word dilation - To seperate words
## Find Contours -  To get higher areas which symbolise words with a threshold on contour area
- RETR_EXTERNAL - Gives only external contours
- CHAIN_APPROX_SIMPLE - Gives 4 corners of the contour




# Task 3 - Template Matching
Matching the digits on a cheque number with their visual representations

## Step 1 - Detecting contours in reference image
- FindContours - we get 22 contours
- Sort contour from left-to-right to match
- Extract digits and symbols to get proper contours i.e from 22 to 14 contours .  Height and width of ROI's are larger 

## Step 2 - Mapping extracted contours to characters

## Step 3 - Extracting contours from cheque image
- Crop the image to get bottom 20-30%
- Blackhat morphological operator - binary inversion with high accuracy
- To remove external borders , use sobel filter
- Apply a closing operation
- clear_border to remove borders
- Dividing into 3 contours and process each individually
- Get ROI's using digit level contour matching
- Matching using cv2.matchTemplate , cv2.minMaxLoc()
    - cv2.matchTemplate - returns an image according to the function given as input
    - cv2.minMaxLoc - finds max area locations