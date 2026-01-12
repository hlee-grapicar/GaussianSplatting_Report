# Gaussian Splatting: From Capture to Reconstruction

## Abstract
*   **Objective:** Document the methodology for 3D scene reconstruction using Gaussian Splatting.
*   **Process:**
    *   Data Acquisition (360° Camera)
    *   Image Preprocessing
    *   Structure from Motion (SfM)
    *   Gaussian Point Cloud Optimization
*   **Content:** Details tools, parameters, and system specifications.
*   **Key Finding:** Processing limitations were identified and addressed.

## Introduction
*   **Purpose:** Document the end-to-end workflow for a Gaussian Splatting 3D scene reconstruction.
*   **Scope:** From initial video capture to the final optimized Gaussian point cloud.
*   **Focus:** Procedural account of tools, configurations, and key decisions.

## System Specifications
*   **Device:** DESKTOP-GF31VVN
*   **CPU:** 13th Gen Intel(R) Core(TM) i7-13620H @ 2.40 GHz
*   **RAM:** 32.0 GB
*   **GPU:** NVIDIA GeForce RTX 4060 Laptop GPU
*   **VRAM:** 8.0 GB (Dedicated)

## Methodology: Data Acquisition
*   **Hardware:** Insta360 X5 Camera
*   **Mode:** Equirectangular 360° Video
*   **Initial Processing:** Insta360 Editor
    *   **Export Format:** 360 Video (MP4)
    *   **Stabilization:** Direction Lock enabled to ensure consistent orientation.
*   **Note:** A single camera was used due to hardware limitations, differing from multi-camera recommendations.

## Recommendations: Data Acquisition
*   **Lens:** Use a lens with minimal distortion effects.
*   **Camera Mode:** Use manual mode to ensure consistent settings (exposure, focus, white balance) across all captures.
*   **Capture Method:**
    *   Prioritize still photographs over video to avoid motion blur.
    *   If using video, ensure smooth and gentle camera movement.
*   **Shooting Strategy:**
    *   Begin with object-centric captures, as they tend to yield better results.
    *   Proceed to background or indoor scenes after validating the initial process.

## Methodology: Image Preprocessing
*   **Software:** Blender with 360 Extractor addon.
*   **Process:** A virtual camera extracted cropped views from the 360° video.
*   **Configuration:**
    *   **Output Resolution:** 1920x1920 pixels
    *   **Aspect Ratio:** 1:1
*   **Reason:** This ratio is recommended for optimal performance in the Gaussian Splatting pipeline.

## Methodology: Structure from Motion (SfM)
*   **Software:** COLMAP (Open-source SfM/MVS pipeline).
*   **Input:** Preprocessed 1920x1920 images.
*   **Key Operations:**
    *   Feature identification and matching.
    *   Camera pose estimation (intrinsic/extrinsic parameters).
    *   Sparse 3D point cloud reconstruction.
*   **Output:** Camera parameters and sparse point cloud for the next stage.

## Methodology: Gaussian Splatting Generation
*   **Software:** PostShot.
*   **Input:** COLMAP project data (camera poses & sparse point cloud).
*   **Process:**
    *   Optimized a set of Gaussian primitives to represent the scene.
    *   Iteratively refined position, color, opacity, and covariance via gradient descent.
*   **Output:** A high-fidelity, renderable, optimized Gaussian point cloud.

## Results and Discussion
*   **Processing Challenge:**
    *   Initial attempts to process ~1000 images with COLMAP led to instability on Windows and prohibitive processing times on Ubuntu.
*   **Solution:**
    *   The image set was reduced to ~300 frames, which enabled successful processing.
    *   This corresponds to 30 seconds of footage (5 virtual cameras @ 2 fps).
*   **Rendering Validation:**
    *   The final optimized Gaussian point cloud should be validated by rendering both:
        *   **Training Views:** Images used during the optimization process.
        *   **Test/Novel Views:** New viewpoints not seen during optimization, to assess generalization.
    *   *(Note: The current process should be clarified whether it uses a train/test split or optimizes on all images before rendering novel views.)*

## Conclusion
*   **Outcome:** Successfully reconstructed a 3D scene as an optimized Gaussian point cloud from a single 360° video.
*   **Workflow:** Utilized a pipeline of specialized tools (Insta360 Editor, Blender, COLMAP, PostShot).
*   **Key Finding:** Input image quantity must be balanced with hardware capabilities for the SfM stage.
*   **Viability:** The process is a viable method for generating Gaussian point clouds with consumer-grade hardware.

## Future Work: Workflow Improvements
*   **Improve Accuracy with Manual COLMAP Configuration:**
    *   **Hypothesis:** Providing COLMAP with known camera rig information from the 360 Extractor will improve reconstruction accuracy.
    *   **Action:**
        1.  Generate a reconstruction *with* manual COLMAP rig parameters.
        2.  Generate a baseline reconstruction *without* manual parameters.
        3.  Render the same novel views from both resulting point clouds.
    *   **Evaluation:** The two outputs will be compared quantitatively using the following perceptual metrics:
        *   **PSNR (Peak Signal-to-Noise Ratio):** Measures pixel-level error. Higher is better.
        *   **SSIM (Structural Similarity Index Measure):** Measures perceived structural similarity. Closer to 1 is better.
        *   **LPIPS (Learned Perceptual Image Patch Similarity):** Measures perceptual similarity using a deep learning model. Closer to 0 is better.

## References
*   Insta360 Editor
*   Blender 360 Extractor Addon
*   COLMAP
*   PostShot
