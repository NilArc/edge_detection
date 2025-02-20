# DICOM Image Edge Detection using Computer Vision Techniques

## Overview

This documentation provides an analysis of the problem, the implemented solution to solve the problem, and details on how the solution is implemented in Python. The main goal of this program is to process a DICOM image and detect its edges using computer vision techniques.

## Table of Contents

1. [Problem Analysis](#problem-analysis)
2. [Implemented Computer Vision Techniques](#implemented-computer-vision-techniques)
3. [Solution Implementation](#solution-implementation)
4. [Sample Case](#sample-case)

## Problem Analysis

In the medical field, accurate diagnosis of a patient’s condition, especially for organs such as the lungs, is crucial. Traditional diagnostic methods might require surgical procedures to obtain samples, posing risks to the patient. An alternative is to use processed images for diagnosis, which is less invasive and safer.

However, medical images often contain noise or have poor visibility in areas of interest. Therefore, it's necessary to highlight the Region of Interest (ROI) in the image. This project uses "Lung X-ray Chest PA only" images from TCIA in DICOM format to achieve this goal.

## Implemented Computer Vision Techniques

This project incorporates several computer vision techniques to detect edges and highlight the ROI in lung images:

1. **Otsu’s Thresholding**: Converts grayscale images to binary form.
2. **Median Filtering**: Reduces noise in the image.
3. **Canny Edge Detection**: Detects edges in the image.
4. **Hough Transformation**: Identifies straight lines in the image.
5. **Dilation**: Thickens lines in the image.
6. **Contours**: Visualizes the boundaries of the ROI.
7. **Jaccard Similarity Index**: Evaluates the closeness of the resulting image to the original image.

## Solution Implementation

### Requirements

1. Access to Google Collaboratory
2. Install the following library dependencies:
   - Pydicom
   - Numpy
   - Skimage
   - Matplotlib
   - OpenCV Python

### Implementation Steps

The steps identified in the "Implemented Computer Vision Techniques" section are implemented through functions:

| Technique            | Description                                                                                                                                 | Usage                                    | Parameters                                                                                     | Return                                            |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------|------------------------------------------------------------------------------------------------|---------------------------------------------------|
| Otsu’s Thresholding  | Converts grayscale image to binary form (Jadwaa, 2022)                                                                                      | `apply_otsu_threshold(image)`            | `image` (numpy.ndarray)                                                                         | Binary image (numpy.ndarray)                     |
| Median Filter        | Removes noise from an image (Jadwaa, 2022)                                                                                                  | `apply_median_filter(image, kernel_size)` | `image` (numpy.ndarray), `kernel_size` (int, default = 50)                                      | Filtered image (numpy.ndarray)                   |
| Canny Edge Detection | Combines Gaussian smoothing, gradient computation, non-maxima suppression, and double-threshold detection for accurate edge detection (Jadwaa, 2022) | `apply_canny_edge_detector(image, low_threshold, high_threshold)` | `image` (numpy.ndarray), `low_threshold` (int, default = 1), `high_threshold` (int, default = 1) | Edges (numpy.ndarray)                             |
| Hough Transformation | Detects straight lines in an image. Usually used with the output of the Canny edge detector (Gilewski, 2022)                                  | `hough_line(median_filtered_image, image_copy)` | `median_filtered_image` (numpy.ndarray), `image_copy` (numpy.ndarray)                         | Line Image (numpy.ndarray) - merged with original image |
| Dilation             | A morphological process that thickens lines (Gilewski, 2022)                                                                                 | `post_process(edge)`                     | `edge` (numpy.ndarray) - result image of Canny edge detector                                   | Result (numpy.ndarray)                            |
| Evaluation           | Evaluates the closeness of images using the Jaccard Similarity Index                                                                          | `eval(image1, image2)`                   | `image1` (numpy.ndarray), `image2` (numpy.ndarray)                                              | Jaccard Similarity Index (float)                 |

### Sample Case

The image used (9a10650e-5e39-474b-a741-72b6ae0a311f.dcm) was downloaded from TCIA. It is an X-ray Chest PA of a patient.

#### Testing the Functions with the Actual Image

The images below show the Jaccard Similarity Index of the original and resulting image, and three images: the original input image, the edge detected by the Canny edge detector, and the result of the Hough transformation.

---

For more details on the implementation, please refer to the code provided in the project repository.