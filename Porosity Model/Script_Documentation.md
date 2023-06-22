## Porosity Calculation Documentation

This code provides a function `calculate_porosity` to calculate the porosity percentage of an image based on a brightness threshold. The porosity percentage represents the percentage of pore pixels in the image.

### Prerequisites

- This code requires the installation of the OpenCV library (and the `cv2_imshow` function from the `google.colab.patches` module for working on Google Colaboratory)
- The code assumes that the image file is in either PNG or JPG format.

### Function Signature

```python
def calculate_porosity(image_path, brightness_threshold):
```

### Input Parameters

1. `image_path` (string): The path to the image file (PNG or JPG) on which the porosity calculation will be performed.
2. `brightness_threshold` (integer): The brightness threshold value to convert the image to binary. Pixels below this threshold will be considered as pore pixels.

### Output

- The function returns the calculated porosity percentage as a float value.

### Process Overview

1. Read the image file using OpenCV and convert it to grayscale.
2. Apply a Gaussian blur filter to reduce noise in the image.
3. Convert the grayscale image to binary based on the brightness threshold using OpenCV's `threshold` function.
4. Display the binary image using the `cv2_imshow` function from the `google.colab.patches` module.
5. Count the number of pore pixels in the binary image using OpenCV's `countNonZero` function.
6. Calculate the total number of pixels in the image.
7. Calculate the porosity percentage by dividing the number of pore pixels by the total number of pixels and multiplying by 100.
8. Return the porosity percentage.

### Usage

1. Import the necessary libraries:
   ```python
   import cv2
   from google.colab.patches import cv2_imshow
   ```

2. Define the `calculate_porosity` function and provide the image path and brightness threshold as input parameters. The function will return the porosity percentage.
   ```python
   def calculate_porosity(image_path, brightness_threshold):
       # Function implementation
       return porosity_percentage
   ```

3. Specify the path to your image (PNG or JPG):
   ```python
   image_path = "Sample Image.jpg"
   ```

4. Set the brightness threshold (adjust as needed):
   ```python
   brightness_threshold = 73
   ```

5. Call the `calculate_porosity` function with the image path and brightness threshold:
   ```python
   porosity_percentage = calculate_porosity(image_path, brightness_threshold)
   ```

6. Print the result:
   ```python
   print("Porosity percentage: {:.2f}%".format(porosity_percentage))
   ```

### Output

```python
import cv2
from google.colab.patches import cv2_imshow

def calculate_porosity(image_path, brightness_threshold):
    image = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)
    image = cv2.GaussianBlur(image, (15, 15), 0)

    _, binary_image = cv2.threshold(image, brightness_threshold, 255, cv2.THRESH_BINARY)
    cv2_imshow(binary_image)

    pore_pixels = image.size - cv2.countNonZero(binary_image)

    total_pixels = image.size
    porosity_percentage = (pore_pixels / total_pixels) * 100

    return porosity_percentage

image_path = "Sample Image.jpg"
brightness_threshold = 73

porosity_percentage = calculate_porosity(image_path, brightness_threshold)

print("Porosity percentage: {:.2f}%".format(porosity_percentage))
```
![image](https://github.com/hsr-22/SoC-2023-ImageProcessing-and-ObjectDetection/assets/112925148/82e4f533-b656-4745-a95c-09120b182849)
Porosity percentage: 31.54%

In this example, the code calculates the porosity percentage of the image "Sample Image.jpg" with a brightness threshold of 73. The resulting porosity percentage is then printed to the console.

## RESULT : **Porosity percentage (Sample Image) = 31.54%**
