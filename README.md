# Lunar Post-Capture Alignment and Stacking
## An Earth-Based Computer Vision Approach

![License](https://img.shields.io/github/license/chase-kusterer/astrophotography)

## Introduction
This project innovates in its approach to lunar astrophotography through advanced computer vision techniques. Its objective is to process video frames into ultra-sharp composite images of the Moon, utilizing a custom crater reference map and lucky imaging. Alignment and crater detection tuning are applied automatically, but can be customized as needed. The resulting images are fully based on the provided video frames; no part of the final images are AI-generated.
<br><br>

## Quick Start
Upload an MP4 to the <code>lunar_videos</code> folder and run the <code>Lunar_Post_Capture</code> notebook. A sample lunar video has been provided in case you don't have a lunar video on hand. Once processed, stacked images will be available in the <code>stacks</code> folder. Artifacts can be found in the <code>lunar_stack_artifacts</code> folder.
<br><br>

## Project Walkthrough
Earth-based astrophotography suffers from equipment jitter and atmospheric turbulence.
<br><br>

<p align="center">
  <details>
    <summary>Lunar Drift Clip</summary>

  <video src="https://github.com/user-attachments/assets/7eddcd9b-866b-478b-80d4-7e7400f57a8e"></video>

  </details>
  
</p>
<br>

The first step in solving this challenge is frame alignment. 
To align frames properly, a crater reference map has been developed from a reference mosaic of 1,300 image captures from the <a href="https://lroc.im-ldi.com/visit/exhibits/1/gallery/17">Lunar Reconnaissance Orbiter Camera</a> and the <a href="https://www.kaggle.com/datasets/sujaykapadnis/moon-crater-database-v1-robbins">Robbins Lunar Crater Database</a>. Mapping has been limited to 295 craters in eight highly-visible maria to avoid detection anomalies that commonly occur near the Moon's limb and terminator.
<br><br>

<p align="center">
  <img src="assets/images/crater_reference_map.png" width="500" alt="Crater Reference Map">
</p>

To align with the crater reference map, Meta's lightweight ViT-B Segment Anything Model (SAM) is applied to segment the lit portion of the Moon in each video frame, as well as the reference mosaic. Captured frames are then rescaled through RANSAC circle fitting.
<br><br>

<p align="center">
  <img src="assets/images/lunar_pipeline_1x3.png" width="600" alt="Lunar Pipeline">
</p>

Starting at the center of the lit portion of the moon in the sharpest captured frame, craters are detected using Laplacian-of-Gaussian Blob Detection (LoG). Detection is hypertuned for optimal alignment based on the n-closest craters, crater diameter, and crater magnification. Finally, captured frames are fine tuned through rotation.
<br><br>

<p align="center">
  <img src="assets/images/centroid_based_alignment.png" width="800" alt="Centroid-Based Alignment">
</p>

Resulting in a crisp, ultra-sharp image of the moon!
<br>
<p align="center">
  <img src="assets/images/median_moon_composite.png" width="400" alt="Median Moon Composite">
</p>
<br>

## Computer Vision Techniques
* Segment Anything Model (SAM)
* Laplacian-of-Gaussian Blob Detection (LoG)
* RANSAC Circle Fitting
* Centroid-Based Alignment
<br><br>

## Project Architecture
<p align="center">
  <img src="assets/images/project_architecture.png" width="300" alt="Project Architecture">
</p>

<br>

## Additional Resources
A technical synopsys is available in the <code>documentation</code> folder.

---

## License

MIT License. See [LICENSE](LICENSE) for details.
