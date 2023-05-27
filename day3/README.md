# Convex Optimization
- CVXPY Library - Optimization problems
- Minimize f0x , subject to f1y < b
- Stanford lectures on Optimisation
- Study about convex functions
## **Problem** : Smoothen a noisy signal
    - It is a optimization problem where you have to design another smoothed signal array of points such that they contain information of the original signal but are relatively smooth
    - For this we can first minimise the mean_squared_error between the generated and new signal points to clone the signal
    - Then we add a regularisation term which can be either L1 or L2 terms of 1st , 2nd or 3rd order
        - L1 regularisation tries to sparse the terms to obtain smoothed regions
        - L2 regularisation kind of spreads the loss always trying to reduce it giving the new signal a curved shape
        - 1st order = velocity , 2nd order = acceleration , 3rd order = Jerk

## **Problem** : Smoothen the movements of bounding boxes formed over middle shots of characters in a video
    - This is similar to smoothening the signal by reducing noise
    - We can apply a similar transformation to the x and y coordinate of the centre of the bounding box along with the size/height of the bounding box
    - This will give a more stable bounding box

# Medical Imaging
- Modalities
    - visible light
    - UltraSound
    - X-ray
    - Nuclear (gamma rays)
    - MRI
    - CTC 
    - Microscopy

- What is being imaged ? 
    - Living organism ; In-vivo imaging
    - It is a 3D or Volume Image
    - Slicing
        - Axial
        - Sagettal
        - Coronal
    - To access more information , we include other dimensions

- Radon Transform
- Simple Backprojection