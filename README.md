# Object Detection & Recognition using Template Matching in OpenCV-Python

<div class="row">
  <div class="column">
    <img src="figures/template-matching--002.webp" width="500">
  </div>
</div>

## 1. Objective

The objective of this project is to demonstrate object localization via template matching using OpenCV-Python built-in functionalities. 

## 2. Template Matching

Template matching is a technique for finding areas of an image that are similar to the template of an object of interest, such as a person, vehicle, animal, etc. The goal of template matching is to detect and localize the template image (T) in a source image S:

* The source Image (S), which is the image where the template may be localized
* The template Image (T), which is the image that is to be found in the source image.

Template matching is useful when the shape, orientation and scale of the object of interest in the new imaged scene rains almost the same as what is captured in its template image. Most fixed-template matching approach are based on computing a cross-similarity metric between the template and target images and detecting any peaks in the metric values. In particular, template matching apply a sliding window over all the pixels in the source image order to detect the position of cross-similarity metric peak value between a template and template-size patches of target image, at each of its pixels, and locate the best match, if the template image is present in the target image. The absence of such a significant peak indicates that the template image is likely not present in the target image.

### 2.1 Methodology

The applied template matching process can be outlined as follows:

* The template image simply slides over the input image (as in 2D convolution) 
* The template and patch of input image under the template image are compared.
* The result obtained is compared with the threshold
* If the result is greater than threshold, the portion will be marked as detected.

### 2.2 OpenCV Python API

The OpenCV Python API for the template matching functionality is as follows:
```
result=cv.matchTemplate(image, templ, method[, result[, mask]]) 
```

The Parameters are as follows:

1. Input:

* image: Image where the search is running. 
* template: Searched template. It must be not greater than the source image and have the same data type.
* result: Map of comparison results. If image is W×H  and template is w×h then result is (W−w+1)×(H−h+1)
* method: Parameter specifying the comparison method
  * The cross-similarity between the template and source image patch can be assessed based in several suitable metrics, which can be grouped as follows:
    * Mean squared error with or without normalization 
    * Cross correlation with or without normalization
  * OpenCV offers the six matching metrics, please see TemplateMatchModes for more information.
* mask: Optional mask. It must have the same size as template. 


2. Output:

* result: Map of comparison results. It must be single-channel 32-bit floating-point. If image is W×H  and template is w×h, then result is (W−w+1)×(H−h+1)

## 3. Data

The template and source images used to demonstrate the template matching development process are illustrated next.

## 4. Template Matching Detection Applications

<div class="row">
  <div class="column">
    <img src="figures/stanford_template_matching.jpg" width="500">
  </div>
</div>

The cross-similarity between the target image T and the reference image I can be assessed based in several suitable mtrics:

* Mean squared error with or without normalization
* Cross correlation with or without normalization

OpenCV offers the following 6 template matching modes:

```
Enumerations
enum  	cv::TemplateMatchModes {
  cv::TM_SQDIFF = 0,
  cv::TM_SQDIFF_NORMED = 1,
  cv::TM_CCORR = 2,
  cv::TM_CCORR_NORMED = 3,
  cv::TM_CCOEFF = 4,
  cv::TM_CCOEFF_NORMED = 5
}
 	type of the template matching operation More...
```

### 3.1. Exploring the Different Smiliarity Metrics

We explored the differnt similarity metrics used for template matching:
  * The normalized cross-correlation heat-map between the template and reference images illustrated in the fogure below. 
  *  Note that higher cross-correlation sub-regions (windows) are associated with the correct location of the template image (window) in the reference image. 

<div class="row">
  <div class="column">
    <img src="figures/stanford_template_matching_cc.jpg" width="800">
  </div>
</div>

### 3.2. Sample Results - Nomalized Cross-Correlation

<table>
  <tr>
    <td align="center"> </td>
    <td align="center"> Template </td>
    <td align="center"> Template Matching Results</td>
  </tr> 
  <tr>
    <td> Window </td>
    <td> <img src="figures/pillar.jpg" width="50"  > </td>
    <td> <p align="center"><img src="figures/stanford_template_matching_results.JPG" width="500"></p>/td>
  </tr>
  <tr>
    <td> Right Kitten </td>
    <td> <img src="figures/right_kitten.jpg" width="50"  > </td>
    <td> <p align="center"><img src="figures/cats_template_matching_results.JPG" width="200"></p></td>
  </tr>
  <tr>
    <td> Messi </td>
    <td> <img src="figures/messi.jpg" width="50"  > </td>
    <td> <p align="center"><img src="figures/barcelona_messi_template_matching_results.JPG" width="500"></p></td>
  </tr>
</table>

### 3.3. Idenified Limitations

The limitations of pixel-based object detection approaches are very similar to those of pixel-based image stitching techniques. As such they tend to be computationally expensive as they process all image pixels, they are also sensitive to changes in illumination, scale and orientation. Furthermore, pixel-based template matching is sensitive to occlusion, as the object needs to be fully visible in the scene image to be detected. These techniques are more suitable for restricted environments where imaging conditions, such as image intensity and viewing angles between the template and images containing this template are the same. However, recently pixel-based template-matching techniques, which are less sensitive to variations in orientation, scale, translation, brightness and contrast have been proposed with some reported success.


## 4. Analysis

We have demonstrated that template matching works well for detecting a fixed-template from a course, acquired under similar conditions. However, template matching has several limitations, including:


* Sensitive to changes in illumination, scale and orientation.
* Sensitive to occlusion, as the object needs to be fully visible in the scene image to be detected.
* Pattern occurrences have to preserve the orientation of the reference pattern image.  As a result, it does not work for rotated or scaled versions of the template as a change in shape/size/shear etc. of object with respect to template will give a false match.
* The method is inefficient when calculating the pattern correlation image for medium to large images as the process is time consuming. 
(* Template matching  techniques are more suitable for restricted environments where imaging conditions, such as image intensity and viewing angles between the template and images containing this template are the same. 
* However, recently template-matching techniques, which are less sensitive to variations in scale, translation, brightness and contrast have been proposed with some reported success. 
* For example, multi-scale template matching is able of detect templates at different scales. That is if the size of the source image patch corresponding to the template image has different size and scale than the used template image.


## 5. Future Work

We propose to explore the following issues related to template matching:

* To study and implement multi-scale template matching is able of detect templates at different scales. That is if the size of the source image patch corresponding to the template image has different size and scale than the used template image
* To study and explore deformable template matching, where the appearance of the object of interest changes in the sources images over time, but we only have a single template:
  * For instance, suppose we have a single image, cropped from one of the frames,  of a person walking in a video and we would like to detect this person in different frames. 
  * Clearly, the person appearance, in terms of shape and size and scale, is expected to vary from frame to frame.
  * We cannot reliably detect the person in rest of frames from the single template obtained from one frame.
  * We shall explore ways to update the template image after each time it is detected from a frame.
  * This problem is better solved using moving object tracking but it will be interesting to explore it using adaptive template matching.

## 6. References

1. OpenCV. Template Matching. Retrieved from: https://docs.opencv.org/master/d4/dc6/tutorial_py_template_matching.html (October 9, 2022). 
2. OpenCV. Template Matching. Retrieved from: https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_template_matching/py_template_matching.html (October 9, 2022).
3. OpenCV. Template Matching. Retrieved from: https://www.ccoderun.ca/programming/doxygen/opencv_3.2.0/tutorial_template_matching.html (October 9, 2022).
4. Adrian Rosebrock. Multi-scale Template Matching using Python and OpenCV. Retrieved from: https://www.pyimagesearch.com/2015/01/26/multi-scale-template-matching-using-python-opencv/ (October 9, 2022).
5. Ravindu Senaratne. Object Detection on Python Using Template Matching. Retrieved from: https://towardsdatascience.com/object-detection-on-python-using-template-matching-ab4243a0ca62 (October 9, 2022).
6. SentDex. Template Matching OpenCV Python Tutorial. Retrieved from: https://pythonprogramming.net/template-matching-python-opencv-tutorial/ (October 9, 2022).
7. Strahinja Zivkovic. Template matching using OpenCV in Python. Retrieved from: http://datahacker.rs/014-template-matching-using-opencv-in-python/ (October 9, 2022).
8. GeeksforGeeks. Template matching using OpenCV in Python. Retrieved from: https://www.geeksforgeeks.org/template-matching-using-opencv-in-python/ (October 9, 2022).

