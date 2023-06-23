# Documentation for Object Detection and Measurement

This documentation explains the code provided for object detection and measurement using computer vision techniques. The code utilizes the `cvlib` library and OpenCV (`cv2`) to detect objects in an image and measure their areas.

## Prerequisites
You can install the necessary libraries using pip:
```
pip install opencv-python
pip install cvlib
pip install matplotlib
```

## Object Detection
The `count_object` function is responsible for detecting objects in an image using the YOLOv4 model. Here's how the code works:

1. Import the required libraries:
```python
import cv2
import matplotlib.pyplot as plt
import cvlib as cvl
from cvlib.object_detection import draw_bbox
```

2. Load and display the image:
```python
img = cv2.imread('toucan.jpg')
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.xticks([]), plt.yticks([])  # to hide tick values on X and Y axis
plt.show()
```

3. Define the `count_object` function to count and display objects in the image:
```python
def count_object(img):
  # Detect common objects in the image
  box, labels, count = cvl.detect_common_objects(img, confidence=0.5, nms_thresh=0.5, model='yolov4', enable_gpu=False)
  
  # Draw bounding boxes around the detected objects
  output = draw_bbox(img, box, labels, count)
  
  # Print the number and labels of the detected objects
  print('Number of objects:', len(labels))
  print('Labels of the objects:', labels)
  
  # Display the image with bounding boxes
  plt.imshow(cv2.cvtColor(output, cv2.COLOR_BGR2RGB))
  plt.xticks([]), plt.yticks([])  # to hide tick values on X and Y axis
  plt.show()
```

4. Call the `count_object` function with the loaded image:
```python
count_object(img)
```

The output will show the number of objects detected and their corresponding labels along with the image displaying the bounding boxes around the objects.

## Object Area Measurement
The `measure_object_area` function measures the area of an object in an image using the following steps:

1. Import the required libraries:
```python
import cv2
import matplotlib.pyplot as plt
```

2. Define the `measure_object_area` function:
```python
def measure_object_area(image_path):
  # Load the image
  image = cv2.imread(image_path)

  # Convert the image to grayscale
  gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

  # Apply inverse binary thresholding to obtain an inversed binary image using Otsu thresholding method
  _, binary = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY_INV | cv2.THRESH_OTSU)

  # Find contours in the binary image
  contours, hierarchies = cv2.findContours(binary, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

  total_area = 0
  # Iterate through each contour
  for contour in contours:
    # Calculate the area of each contour
    area = cv2.contourArea(contour)
    total_area += area

  # Print the measured area
  print("Object area:", total_area)
  plt.imshow(binary, cmap='gray')
```

3. Set the image path and call the `

measure_object_area` function:
```python
image_path = "cube.jpg"
plt.imshow(cv2.cvtColor(cv2.imread(image_path), cv2.COLOR_BGR2RGB))
measure_object_area(image_path)
```

The code will load the image, convert it to grayscale, apply inverse binary thresholding using the Otsu method, find contours, calculate the area of each contour, and print the measured area.

The output will display the loaded image, the binary image after thresholding, and the measured area of the object in the image.
