
# Skin Segmentation Project

## Overview
This project implements a skin segmentation algorithm using OpenCV and NumPy in Python. It processes images to identify and isolate skin regions based on a statistical model derived from training images. The algorithm employs a multivariate Gaussian distribution to classify pixels as skin or non-skin using Mahalanobis distance.

## Prerequisites
To run this code, you need the following dependencies:

- Python 3.x
- OpenCV (cv2)
- NumPy
- Matplotlib

You can install the required packages using pip:

```
pip install opencv-python numpy matplotlib
```

## Project Structure

- **skin_segmentation.py**: The main Python script implementing the skin segmentation algorithm.
- **Input Images**: The code expects training images (`img11.jpg`, `img12.jpg`, `img13.jpg`) and test images (`img4.jpg`, `img6.jpg`) in the `/content/` directory.
- **Output**: Processed images with skin segmentation are saved with the prefix `skin_` (e.g., `skin_img4.jpg`).

## Algorithm

### Training Phase:
1. Loads training images specified in `train_paths`.
2. Extracts non-white pixels from these images to form a dataset of skin pixels.
3. Computes the mean vector and covariance matrix of the skin pixel values in RGB space.
4. Calculates the inverse covariance matrix for Mahalanobis distance calculations.

### Testing Phase:
1. Loads test images from `test_paths`.
2. For each pixel in a test image, computes the Mahalanobis distance to the skin pixel distribution.
3. If the distance is below a threshold (default: 6.0), the pixel is classified as skin and retained; otherwise, it is set to white.
4. Displays the original and segmented images side-by-side using Matplotlib.
5. Saves the segmented image to disk.

## Usage

1. Place your training and test images in the `/content/` directory.
2. Update the `train_paths` and `test_paths` lists in the code with the correct image file paths if needed.
3. Run the script:

```
python skin_segmentation.py
```

4. Check the output images in the working directory and the displayed plots.

## Customization

- **Threshold Adjustment**: Modify the threshold parameter in the `segment_skin` function call (default: 6.0) to fine-tune segmentation sensitivity.
- **Training Data**: Add more training images to improve the skin model's accuracy across different skin tones and lighting conditions.
- **File Paths**: Update the image paths in `train_paths` and `test_paths` to use your own directory structure.

## Performance Optimization

For large images or when processing multiple files, consider these optimizations:

- Use NumPy vectorized operations instead of pixel-by-pixel iteration.
- Implement multiprocessing for parallel image processing.
- Resize large images before processing to improve speed.

## Limitations

- The algorithm relies on the quality and representativeness of the training images.
- Lighting conditions and skin tone variations may affect performance.
- The code processes static images and is not optimized for real-time video processing.
- The simple statistical model may produce false positives in areas with skin-like colors.

## Future Improvements

- Add support for video processing and real-time segmentation.
- Implement a more robust skin detection model using machine learning approaches (e.g., CNN, Random Forest).
- Add pre-processing filters to handle various lighting conditions.
- Create a command-line interface with adjustable parameters.
- Incorporate post-processing techniques to reduce noise and improve boundary detection.
