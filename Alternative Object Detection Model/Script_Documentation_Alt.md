## Documentation for Object Detection

The provided code performs image processing operations on an image of objects to detect and count the number of objects present. It uses the OpenCV (cv2) library, numpy, and matplotlib for image manipulation and visualization.

### 1. Import Required Libraries
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
- **cv2**: OpenCV library for computer vision tasks.
- **numpy**: Library for numerical operations in Python.
- **matplotlib**: Library for data visualization.

### 2. Load the Image
```python
image = cv2.imread('image-path')
```
- Reads the image using the `cv2.imread()` function and assigns it to the variable `image`.

### 3. Convert Image to Grayscale
```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
- Converts the loaded image to grayscale using the `cv2.cvtColor()` function with the `cv2.COLOR_BGR2GRAY` conversion flag.
- The grayscale image is stored in the variable `gray`.

### 4. Display Grayscale Image
```python
plt.imshow(gray, cmap='gray')
```
- Displays the grayscale image using `plt.imshow()` function from matplotlib.
- The colormap 'gray' is specified to visualize the image in grayscale.

### 5. Apply Gaussian Blur
```python
blur = cv2.GaussianBlur(gray, (13, 13), 0)
```
- Applies Gaussian blur to the grayscale image using the `cv2.GaussianBlur()` function.
- The kernel size is defined as (13, 13) to specify the blurring strength.
- The blurred image is stored in the variable `blur`.

### 6. Display Blurred Image
```python
plt.imshow(blur, cmap='gray')
```
- Displays the blurred image using `plt.imshow()` function.
- The colormap 'gray' is specified to visualize the image in grayscale.

### 7. Apply Canny Edge Detection
```python
canny = cv2.Canny(blur, 30, 150, 3)
```
- Applies Canny edge detection to the blurred image using the `cv2.Canny()` function.
- The parameters 30 and 150 define the low and high thresholds for edge detection.
- The last parameter, 3, specifies the aperture size for the Sobel operator.
- The resulting edge-detected image is stored in the variable `canny`.

### 8. Display Canny Edge Image
```python
plt.imshow(canny, cmap='gray')
```
- Displays the Canny edge image using `plt.imshow()` function.
- The colormap 'gray' is specified to visualize the image in grayscale.

### 9. Dilate the Edges
```python
dilated = cv2.dilate(canny, (1, 1), iterations=0)
```
- Dilates the edges in the Canny edge image using the `cv2.dilate()` function.
- The `(1, 1)` kernel is used for dilation.
- The resulting dilated image is stored in the variable `dilated`.

### 10. Display Dilated Image
```python
plt.imshow(dilated, cmap='gray')
```
- Displays the dilated image using `plt.imshow()` function.
- The colormap 'gray' is specified to visualize the image in grayscale.

### 11. Find Contours
```python
cnt, hierarchy = cv2.findContours(dilated.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)
```
- Finds contours in the dilated image using the `cv2.findContours()` function.
- The `dilated.copy()` is passed as the input image.
- The `cv2.RETR_EXTERNAL` retrieval mode retrieves only the external contours.
- The `cv2.CHAIN_APPROX_NONE` contour approximation method retrieves all the contour points.
- The resulting contours are stored in the variables `cnt` (contours) and `hierarchy` (contour hierarchy information).

### 12. Convert Image to RGB
```python
rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```
- Converts the original BGR image to RGB format using the `cv2.cvtColor()` function.
- The RGB image is stored in the variable `rgb`.

### 13. Draw Contours on the RGB Image
```python
cv2.drawContours(rgb, cnt, -1, (0, 255, 0), 2)
```
- Draws the contours on the RGB image using the `cv2.drawContours()` function.
- The `rgb` image is modified in-place.
- The `cnt` variable containing the contours is passed as input.
- The `(0, 255, 0)` color specifies green color for drawing the contours.
- The last parameter, 2, defines the thickness of the contour lines.

### 14. Display Final Image with Contours
```python
plt.imshow(rgb)
```
- Displays the final image with drawn contours using `plt.imshow()` function.

### 15. Count the Number of Contours
```python
print("Objects in the image : ", len(cnt))
```
- Prints the number of contours (representing objects) detected in the image using `len(cnt)`.

This code provides a step-by-step process for loading an image, converting it to grayscale, applying Gaussian blur, performing edge detection, dilating the edges, finding contours, and visualizing the result. The final output is the original image with the detected contours, along with the count of objects in the image.
