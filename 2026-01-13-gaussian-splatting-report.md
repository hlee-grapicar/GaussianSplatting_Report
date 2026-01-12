# Gaussian Splatting Report: From Capture to Reconstruction

## 1. Introduction
This report details the process of generating a 3D reconstruction using Gaussian Splatting, starting from initial data capture to the final splat generation. The objective is to outline the methodology employed, tools utilized, and specific parameters configured at each stage.

## 2. Data Acquisition
The initial data for this Gaussian Splatting project was acquired using an **Insta360 X5 camera**. The camera was operated in **Equirectangular 360 camera mode**, capturing a full spherical view of the environment. The raw footage from the camera was first processed using the **Insta360 Editor** software. During the export process, it is crucial to select the option to export as **360 videos** and to make sure that **Stabilization Type > Direction Lock is turned on** to ensure consistent video orientation. This exported **MP4 video file** then served as the primary source material for subsequent processing steps.

It is worth noting that the introductory video for the Blender 360 Extractor addon suggested capturing footage using three synchronous 360 cameras (positioned high, middle, and low) for optimal results. While the addon's author indicated that separate recordings could also be used, due to hardware limitations, only a single Insta360 X5 camera was utilized for data acquisition in this project.


## 3. Data Preprocessing (Image Extraction and Cropping)
Following data acquisition, the raw MP4 video was processed to extract individual frames and prepare them for 3D reconstruction. This preprocessing step involved using **Blender** with the **360 Extractor addon**. Within Blender, a virtual camera was configured to crop specific views from the equirectangular footage. A crucial aspect of this stage was setting the virtual camera's output to a **1:1 aspect ratio**, specifically **1920 pixels** in width and height. This particular resolution and aspect ratio were chosen based on recommendations suggesting that a 1:1 ratio is beneficial for subsequent processing steps, leading to a better overall fit in the Gaussian Splatting pipeline.

### Caveats
*   **(Please describe specific issues for this section here)**



## 4. Structure from Motion (SfM) Data Extraction
With the prepared images from the preprocessing stage, **COLMAP** was utilized to perform Structure from Motion (SfM). COLMAP is an open-source MVS (Multi-View Stereo) pipeline that reconstructs 3D scenes and estimates camera poses from a set of ordered images. In this phase, COLMAP analyzed the cropped images to:
*   Identify and match common features across multiple views.
*   Estimate the intrinsic and extrinsic parameters of the virtual camera for each image (camera poses).
*   Reconstruct a sparse 3D point cloud representing the geometric structure of the scene.

The output from COLMAP, including the camera parameters and the sparse point cloud, served as critical input for the subsequent Gaussian Splatting generation step.

### Caveats
*   **(Please describe specific issues for this section here)**



## 5. Gaussian Splatting Generation
The final stage of the pipeline involved generating the 3D Gaussian Splats. This was achieved by importing the outputs from COLMAP (camera poses and sparse point cloud) into **PostShot**. PostShot is a platform that takes the SfM data and leverages it to create a dense 3D representation using Gaussian Splatting. The process involved:
*   Loading the COLMAP project, which contains the reconstructed camera positions and the initial sparse point cloud.
*   PostShot then optimized the Gaussian primitives to represent the scene, iteratively refining their position, color, opacity, and covariance to accurately reproduce the input images from novel viewpoints.

This step effectively transformed the structural information derived from COLMAP into a renderable, high-fidelity 3D Gaussian Splatting model.

### Caveats
*   **(Please describe specific issues for this section here)**



## 6. System Specifications
The Gaussian Splatting pipeline was executed on the following system configuration:

*   **Device Name:** DESKTOP-GF31VVN
*   **Processor:** 13th Gen Intel(R) Core(TM) i7-13620H (2.40 GHz)
*   **Installed RAM:** 32.0 GB (31.6 GB usable)
*   **GPU:** NVIDIA GeForce RTX 4060 Laptop GPU
*   **VRAM:** 8.0 GB (Dedicated)
*   **System Type:** 64-bit operating system, x64-based processor
*   **Pen and Touch Support:** No



