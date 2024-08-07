# Day 1

## Numpy Basics
### Manipulate an Image with numpy

First we use matplot lib to import and display the image.

### Invert Image
This function takes 255 and subtracts an image which is already a numpy array.

```
def invert_image(image):
    image_i = 255 - image
    return image_i
```

### Binary Threshold
Uses np.where to set all pixels based on a threshold.  Takes in case, and then two values.  Depending on the result of the case, the current pixel will be replaced with one of the two values.

```
def binary_threshold(image, threshold):
    b_image = np.where(image > threshold, 255, 0)
    return b_image
```

### Transformations

```
return image[:,::-1]
```
Return all rows and reversed columns.

### Edge Detection
Using sobel_x and sobel_y kernels, we can use the convolve function for edge detection along either the x or y axis. 

The function takes an image, pads it so the kernels can fit the edges, and then iterates over each pixel value, extracting a region that matches the given kernel. We multiply the region with the kernel and sum the results to produce a new pixel value.

```
def convolve(image, kernel):
    image_h, image_w, channels = image.shape
    kernel_h, kernel_w = kernel.shape

    pad_h = kernel_h // 2
    pad_w = kernel_w // 2

    padded_image = np.pad(image, ((pad_h, pad_h), (pad_w, pad_w), (0, 0)), mode='constant', constant_values=0)

    output = np.zeros((image_h, image_w, channels))

    for c in range(channels):
        for i in range(image_h):
            for j in range(image_w):
                region = padded_image[i:i+kernel_h, j:j+kernel_w, c]
                output[i,j] = np.sum(region*kernel)

    return output
```
