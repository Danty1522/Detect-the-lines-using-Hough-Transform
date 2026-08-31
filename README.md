# Detecting Lines Using Hough Transform

## Date: 17/08/2026

## Developed By

* **Name:** Chintala Aman Monty
* **Register No:** 212224040054

## Aim

To implement a basic line detection pipeline using OpenCV by detecting straight lines in an image using the Probabilistic Hough Transform.

---

## Learning Objective

* Understand the basic stages of image processing.
* Learn how to convert a color image into grayscale.
* Understand edge detection using the Canny algorithm.
* Learn how the Hough Transform is used for line detection.
* Practice detecting and highlighting lines using OpenCV.

---

## Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

## Algorithm & Explanation

---

### Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

### Step 2: Read the Image

```python
# Read the image using OpenCV

image = cv2.imread('joel_photo.jpeg')
```

### Output

**Original Image:**

<img width="465" height="577" alt="image" src="https://github.com/user-attachments/assets/2efcde5c-cd8a-4b94-9f99-9e9657d9d2ad" />


---

### Step 3: Convert to Grayscale

```python
# Convert the image to grayscale

gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

The original image is converted from the BGR color format into a grayscale image using `cv2.cvtColor()`.

Grayscale conversion simplifies the image and prepares it for edge detection.

### Output

**Grayscale Image:**

<img width="442" height="578" alt="image" src="https://github.com/user-attachments/assets/bb865aa0-ed9e-4129-941a-0f36312efa30" />


---

### Step 4: Edge Detection Using Canny

```python
# Perform Edge Detection

edges = cv2.Canny(gray_image, 50, 150, apertureSize=3)
```

The Canny edge detection algorithm is applied to the grayscale image.

The lower threshold is set to `50` and the upper threshold is set to `150`. The resulting image contains the detected edges.

### Output

**Canny Edge Detection Output:**

<img width="426" height="556" alt="image" src="https://github.com/user-attachments/assets/34e5b2ec-6f0f-4fe1-8b7d-43893a0714d3" />


---

### Step 5: Detect Lines Using Probabilistic Hough Transform

```python
# Detect lines using the probabilistic Hough transform

lines = cv2.HoughLinesP(
    edges,
    rho=1,
    theta=np.pi/180,
    threshold=100,
    minLineLength=50,
    maxLineGap=10
)
```

The Probabilistic Hough Transform is used to detect straight lines from the edge image.

The parameters used are:

* `rho=1` – distance resolution of the accumulator in pixels.
* `theta=np.pi/180` – angular resolution of 1 degree.
* `threshold=100` – minimum number of votes required for a line to be detected.
* `minLineLength=50` – minimum length of a detected line.
* `maxLineGap=10` – maximum gap between line segments that can be joined into a single line.


---

### Step 6: Draw the Detected Lines

```python
# Draw the lines on the original image

output_image = image.copy()

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line
        cv2.line(output_image, (x1, y1), (x2, y2), (0, 255, 0), 2)
```

A copy of the original image is created using `image.copy()`.

If lines are detected, the coordinates of each line are extracted and the lines are drawn on the original image using `cv2.line()`.

The detected lines are displayed in green with a thickness of `2`.

### Output

**Final Line Detection Output:**

<img width="431" height="567" alt="image" src="https://github.com/user-attachments/assets/5b7de6a3-b9ff-41a8-b96c-94f302b391e3" />


---

## Complete Code

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the image using OpenCV
image = cv2.imread('monty.jpeg')

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Perform Edge Detection
edges = cv2.Canny(gray_image, 50, 150, apertureSize=3)

# Detect lines using the probabilistic Hough transform
lines = cv2.HoughLinesP(
    edges,
    rho=1,
    theta=np.pi/180,
    threshold=100,
    minLineLength=50,
    maxLineGap=10
)

# Draw the lines on the original image
output_image = image.copy()

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line
        cv2.line(output_image, (x1, y1), (x2, y2), (0, 255, 0), 2)

# Displaying results using Matplotlib
plt.figure(figsize=(12, 12))

# Input Image and Grayscale Image
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Input Image')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.imshow(gray_image, cmap='gray')
plt.title('Grayscale Image')
plt.axis('off')

# Canny Edge Detection Output
plt.subplot(2, 2, 3)
plt.imshow(edges, cmap='gray')
plt.title('Canny Edge Detector Output')
plt.axis('off')

# Hough Transform Result
plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(output_image, cv2.COLOR_BGR2RGB))
plt.title('Hough Transform - Line Detection')
plt.axis('off')

# Display all results
plt.show()

```
---

## Result

Thus, the line detection pipeline is successfully implemented using OpenCV and the Probabilistic Hough Transform. The system detects straight lines from the edges of the input image and highlights the detected lines on the original image.

---
