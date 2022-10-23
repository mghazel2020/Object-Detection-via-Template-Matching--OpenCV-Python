# Object Detection & Recognition using Template Matching in OpenCV-Python

<div class="row">
  <div class="column">
    <img src="figures/template-matching--002.webp" width="500">
  </div>
</div>

## 1. Objective

The objective of this project is to demonstrate object localization via template matching using OpenCV-Python built-in functionalities. 

2. Template Matching

Template matching is a technique for finding areas of an image that are similar to the template of an object of interest, such as a person, vehicle, animal, etc. The goal of template matching is to detect and localize the template image (T) in a source image S:


* The source Image (S), which is the image where the template may be localized
* The template Image (T), which is the image that is to be found in the source image.


Template matching is useful when the shape, orientation and scale of the object of interest in the new imaged scene rains almost the same as what is captured in its template image. Most fixed-template matching approach are based on computing a cross-similarity metric between the template and target images and detecting any peaks in the metric values. In particular, template matching apply a sliding window over all the pixels in the source image order to detect the position of cross-similarity metric peak value between a template and template-size patches of target image, at each of its pixels, and locate the best match, if the template image is present in the target image. The absence of such a significant peak indicates that the template image is likely not present in the target image.



2.1 Methodology



The applied template matching process can be outlined as follows:

* The template image simply slides over the input image (as in 2D convolution) 
* The template and patch of input image under the template image are compared.
* The result obtained is compared with the threshold
* If the result is greater than threshold, the portion will be marked as detected.

2.2 OpenCV Python API


The OpenCV Python API for the template matching functionality is as follows:

result=cv.matchTemplate(image, templ, method[, result[, mask]]) 

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

3. Data

The template and source images used to demonstrate the template matching development process are illustrated next.

<div class="row">
  <div class="column">
    <img src="figures/stanford_template_matching.jpg" width="500">
  </div>
</div>

The cross-similarity between the target image T and the reference image I can be assessed based in several suitable mtrics:

* Mean squared error with or without normalization
* Cross correlation with or without normalization

OpenCv offers the following 6 template matching modes:

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

### 3.1.1 Exploring the Different Smiliarity Metrics

* TBD: 

  * Explore the differnt similarity metrics used for template matching
  * The normalized cross-correlation heat-map between the template and reference images illustrated in the fogure below. Note that higher cross-correlation sub-regions (windows) are associated with the correct location of the template image (window) in the reference image. 

<div class="row">
  <div class="column">
    <img src="figures/stanford_template_matching_cc.jpg" width="800">
  </div>
</div>


### 3.1.2 Sample Results - Nomalized Cross-Correlation


<table>
  <tr>
    <td> Template </td>
    <td> Template Matching Results</td>
  </tr> 
  <tr>
    <td> Window </td>
    <td> <img src="figures/pillar.jpg" width="50"  > </td>
    <td> <img src="figures/stanford_template_matching_results.JPG" width="500"></td>
  </tr>
  <tr>
    <td> Right Kitten </td>
    <td> <img src="figures/right_kitten.jpg" width="50"  > </td>
    <td> <img src="figures/cats_template_matching_results.JPG" width="200"></td>
  </tr>
  <tr>
    <td> Messi </td>
    <td> <img src="figures/messi.jpg" width="50"  > </td>
    <td> <img src="figures/barcelona_messi_template_matching_results.JPG" width="500"></td>
  </tr>
</table>


### 3.1.3 Limitations

The limitations of pixel-based object detection approaches are very similar to those of pixel-based image stitching techniques. As such they tend to be computationally expensive as they process all image pixels, they are also sensitive to changes in illumination, scale and orientation. Furthermore, pixel-based template matching is sensitive to occlusion, as the object needs to be fully visible in the scene image to be detected. These techniques are more suitable for restricted environments where imaging conditions, such as image intensity and viewing angles between the template and images containing this template are the same. However, recently pixel-based template-matching techniques, which are less sensitive to variations in orientation, scale, translation, brightness and contrast have been proposed with some reported success.


### 3.2 Deformable Template Matching

* TBD: 

* Template matching from videoL
  * Adaptively update the template image
  * Try the video I found on Youtube

### 4 Conclusions

* TBD: 

