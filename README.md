# Object-Recognition-Template-Matching--OpenCV-Python

## 1. Objective

To demonstrate object localization via template matching using OpenCV-Python built-in functionalities.

## 2. Code

## 3. Template Matching

Most pixel-based object detection techniques are based on matching a known template within the target image. Thus, if a template describing a specific object is available, object detection becomes a process of matching features between the template and the image sequence under analysis. There are two types of object template matching, fixed and deformable template matching. Given that our objects of interest are rigid, we shall focus on fixed template matching.

Fixed templates are useful when object shapes do not change with respect to the viewing angle of the camera. Most fixed-template matching approach are based on computing the cross-correlation between the template and target images and detecting any peaks in the correlation values. In particular, these techniques apply a sliding window over all the pixels in order to detect the position of the normalized cross-correlation peak between a template and a target image and locate the best match, if the template image is present in the target image. The absence of such cross-correlation peak indicates that the template image is likely not in the target image. Pixel-based template matching techniques are generally less sensitive to noise and illumination effects in the images [4].

The limitations of pixel-based object detection approaches are very similar to those of pixel-based image stitching techniques. As such they tend to be computationally expensive as they process all image pixels, they are also sensitive to changes in illumination, scale and orientation. Furthermore, pixel-based template matching is sensitive to occlusion, as the object needs to be fully visible in the scene image to be detected. These techniques are more suitable for restricted environments where imaging conditions, such as image intensity and viewing angles between the template and images containing this template are the same. However, recently pixel-based template-matching techniques, which are less sensitive to variations in orientation, scale, translation, brightness and contrast have been proposed with some reported success [5].
