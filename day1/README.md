# Intro to Python and Numpy
- Working with lists and arrays , slicing operations etc
- Most important source is official numpy documentation

# Intro to OpenCV
- Most important source is official opencv documentation
- Image loading , Basic functions 
- Opencv loads image in BGR format
- Image is nothing but a 3-dimensional array containing pixel values with first 2 dimensions being its height and width

# Conversion to grayscale
- Can make different use of the channel pixel values to make the 3D array into a 2D array (or a grayscale image)
- Averaging is 1 method but is not neccessarily intuitive to eyes , instead we can use sensitivity vs wavelength plot to   
  accurately weigh the values of the 3 channels

# Chroma - Keying
- Identifying the distinct pixels in the image to use it for various tasks like fitting an image inside another image

# Thresholding
- It is a technique to fully distinguish the black and white channel in a grayscale image
- cv2.threshold(image, threshold_value, max_value,method) is the opencv library for it . cv2.THRESH_BINARY is generally  
   the method used
- We can use frequency plot of pixels to guess the threshold_value we should use according to the problem

# Barcode Scanning and Detection 

## Barcode Detection
Detecting the barcode from an image which may contain different objects also under the assumption that the barcode is the most prominent region in the image

1. Convert the image to grayscale to have a fewer pixels to analyse and detect
    - *cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)* is the function for it
2. Use **SOBEL** filters to identify edges
    - - Edges are regions of high gradients or intensity changes
    - Sobel filters compute the gradient of intensity change in the x and y direction. 
    - **cv2.Sobel(image, ddepth = cv2.CV_32F, dx, dy , ksize)** is the function  
        - where if dx=1 it calculated horizontal gradient and if dy = 1 , it computes vertical gradient.
    - We then compute final gradient using the euclidean formula
    - Some gradient values are negative and therefore have to be converted to 8-bit unsigned format (0-255)
        - **cv2.convertScaleAbs(gradient)** is the function for it
3. Blurr the image using mean blurring or gaussian blurring to remove uneccessary noise from the image
    - **cv2.blur(image , (3,3))** is the function for mean blurring
    - **cv2.GaussianBlur(image, (3, 3), 0)** is the function for gaussian blurring . 0 is when we want to blur the entire image
4. Performing thresholding on the image with appropriate threshold value
5. Perform a morphological closing operation on the image to close the holes in the image
    - It is basically dilation followed by erosion 
        - Dilation is intensifying of the image which is used to decrease small gaps in bright parts
    - A kernel appropriate for the image is used for it
        - It is created using **cv2.getStructuringElement(cv2.MORPH_RECT, kernel_size)** . It creates a rectangular kernel with the given dimensions 
    - Then , **cv2.morphologyEx(image, cv2.MORPH_CLOSE, kernel)** does the required closing operation with the kernel created in previous step
    - This returns the image with "white" boxes of the detected parts
    - We further dilate the image a bit using **cv2.dilate(closed, None, iterations = 7)** to prevent tight fitting
6. Now , as barcode region is the largest part in the image , we detect the "white" box with the largest area
    - **cv2.findContours(closed.copy(), cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)** finds contours (connected regions) in the image and returns them
    - The contour with the largest area is our barcode
    - **cv2.minAreaRect(contour)** fits a minimum area rectangle over the region with maximum area, hence creating a rectangular bounding box around the barcode
    - **cv2.drawContours** visualises the contour
    - Now we can crop out the image to get the barcode


## Barcode Scanning
There are different methods of it based on different representation of barcode
1. First of all , in a barcode we have to identify the number of '0s' which symbolise a single black point
    - Start of a barcode always contains '101' , therefore using that ,we can identify that
2. Now , with number of 0s representing a bar , we can convert the 'black and white' bars into binarised strings
3. Now , knowing the rep length (Number of binary digits representing a number ) and total number of numbers , we can extract the binary representation of the required digits because a barcode has ``startnum + '101' + 6 numbers + '101' + 6 numbers``
4. Now , using the parity of the encoding numbers in the left half if divided by middle '101' , we can get the encoding pattern
5. Using the encoding pattern , we get the check number