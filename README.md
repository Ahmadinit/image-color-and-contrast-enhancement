# Adaptive Contrast Enhancement Toolkit

**Digital Image Processing Project**

---

## 1. Problem Statement

Many digital images suffer from low contrast due to poor lighting conditions, limited sensor dynamic range, or environmental factors. Low contrast reduces the visibility of important details and structures in an image.

Conventional global enhancement methods, such as histogram equalization, apply a single transformation to the entire image and often fail to preserve local details, leading to over-enhancement or loss of information in certain regions.

---

## 2. Proposed Solution

This project proposes an **Adaptive Contrast Enhancement (ACE) Toolkit** that enhances image contrast by utilizing local image statistics. Instead of applying a global transformation, ACE methods adaptively enhance each pixel based on its surrounding neighborhood.

The toolkit:

- Implements multiple ACE variants
- Supports both grayscale and color images
- Provides an interactive Tkinter-based GUI
- Displays side-by-side comparison of original and enhanced images

---

## 3. Adaptive Contrast Enhancement Framework

Let the input grayscale image be:

$$I(x,y) \in [0, 255]$$

Let:

- $\mu_G$ be the global mean of the image
- $\mu_L(x,y)$ be the local mean in a $w \times w$ window
- $\sigma_L(x,y)$ be the local standard deviation
- $k_1, k_2$ be enhancement control parameters

---

## 4. Implemented Filters and Techniques

### 4.1 Classic Adaptive Contrast Enhancement (ACE)

**Objective:**  
Enhance local contrast while preserving global brightness.

**Mathematical Model:**

$$I_{ACE}(x,y) = k_1 \cdot \frac{\mu_G}{\sigma_L(x,y)} \cdot [I(x,y) - \mu_L(x,y)] + k_2 \cdot \mu_L(x,y)$$

**Explanation:**

- Regions with low local variance receive stronger enhancement
- Maintains overall image brightness using global mean

---

### 4.2 ACE-2 (Simplified ACE)

**Objective:**  
Reduce computational complexity while retaining adaptive behavior.

**Mathematical Model:**

$$I_{ACE2}(x,y) = k_1 \cdot [I(x,y) - \mu_L(x,y)] + k_2 \cdot \mu_L(x,y)$$

**Explanation:**

- Eliminates dependence on local standard deviation
- Faster and suitable for real-time applications

---

### 4.3 Logarithmic ACE-2

**Objective:**  
Enhance low-intensity (dark) regions more effectively.

**Normalization:**

$$I_N(x,y) = 1 - \frac{I(x,y)}{I_{max}}$$

**Enhancement Equation:**

$$I_{Log}(x,y) = k_1 \cdot [\log(I_N(x,y)) - \log(\mu_N(x,y))] + k_2 \cdot \mu_N(x,y)$$

**Explanation:**

- Log transformation expands dark intensity ranges
- Particularly effective for low-light images

---

### 4.4 Exponential ACE-2

**Objective:**  
Provide smooth contrast enhancement with controlled amplification.

**Mathematical Model:**

$$I_{Exp}(x,y) = I_{max} \cdot \left(\frac{I(x,y)}{I_{max}}\right)^{k_1} + \left(\frac{\mu_L(x,y)}{I(x,y)}\right)^{k_2}$$

**Explanation:**

- Uses power-law behavior
- Reduces abrupt intensity changes and noise amplification

---

### 4.5 Color Contrast Enhancement (HLS-Based)

**Objective:**  
Enhance color images without distorting hue information.

**Process:**

1. Convert image from BGR to HLS color space
2. Apply histogram equalization on Saturation
3. Apply linear stretching on Lightness
4. Merge channels and convert back to BGR

**Advantage:**  
Separates contrast enhancement from color information, preserving natural appearance.

---

## 5. Graphical User Interface (GUI)

A Tkinter-based GUI is developed to provide an interactive environment for experimentation.

**GUI Features:**

- Load grayscale or color images
- Adjust ACE parameters (window size, $k_1$, $k_2$)
- Apply different enhancement techniques
- Display original and processed images side-by-side

This enables intuitive understanding of how adaptive enhancement affects image quality.

---

## 6. Results and Comparison

The toolkit visually presents results through side-by-side comparison:

- Original image vs enhanced output
- Comparison between different ACE variants
- Observation of parameter effects on contrast and detail preservation

**Experimental observations show:**

- Classic ACE provides strong enhancement in low-variance regions
- Log-ACE-2 performs best for dark images
- Exp-ACE-2 produces smoother, visually pleasing results
- Color enhancement improves saturation and brightness without color distortion

---

## 7. Tools and Technologies

- **Python**
- **NumPy**
- **OpenCV**
- **Pillow (PIL)**
- **Tkinter**

---

## 8. Conclusion

This project demonstrates the effectiveness of adaptive contrast enhancement over traditional global methods. By integrating multiple ACE variants with a graphical interface, the toolkit serves both as a learning platform and a practical DIP application, allowing users to analyze and compare enhancement techniques interactively.

---

## 9. Group Members

- **Ammar Ahmed** (L200961)
- **Ahmad Naeem** (L216239)

---

## Installation and Usage

### Prerequisites

```bash
pip install numpy opencv-python pillow
```

### Running the Application

```bash
python "Adaptive Contrast  & Color enhancement.py"
```

### How to Use

1. Launch the application
2. Click "Load Image" to select an image file
3. Adjust parameters (Window Size, k1, k2) using sliders
4. Select an enhancement technique from the dropdown
5. Click "Apply Filter" to see the enhanced result
6. View original and enhanced images side-by-side

---
