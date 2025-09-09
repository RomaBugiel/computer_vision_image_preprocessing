# Graphene Image Segmentation Workflow

This repository contains a set of Jupyter notebooks that implement the full pipeline for preparing graphene microscopy images and their segmentation masks, starting from raw images, through ilastik probability maps, to UNet-ready multi-label masks.

## Overview

1. **Image normalization**  
   Notebook: `image_normalization_pipeline.ipynb`  
   - Prepares raw microscopy images for downstream analysis.  
   - Includes intensity normalization, resizing, and consistent formatting.  
   - Ensures reproducibility and standardization of input data.

2. **Probability maps post-processing**  
   Notebook: `ilastik_postprocessing_pipeline.ipynb`  
   - Converts ilastik probability map outputs (`.h5`) into binary masks.  
   - Supports user-defined thresholds and class selection.  
   - Automatically scans directories for `.h5` files and matching raw images.  
   - Exports masks in PNG and NumPy (`.npy`) formats.  
   - Generates overlays and probability heatmaps for quality control.

3. **Label masks post-processing (UNet dataset preparation)**  
   Notebook: `labels_to_unet_masks_pipeline.ipynb`  
   - Processes manually refined ilastik label exports (`*_Labels.h5`).  
   - Fills unlabeled pixels (class 0) using nearest-neighbor interpolation.  
   - Applies morphological smoothing to reduce edge artifacts.  
   - Aligns raw images with masks, builds one-hot multi-label stacks (e.g., *GFM*, *carbonhole*, *undefined*).  
   - Saves paired datasets as images (`.png`) and compressed masks (`.npz`), ready for supervised training.  
   - Performs sanity checks to ensure non-overlapping classes and consistent pixel counts.

## Folder structure

Each notebook defines its own input and output paths, but the workflow is organized around:

- `notebooks/` — Jupyter notebooks for each stage of the pipeline.  
- `data/` — raw images and intermediate outputs.  
- `masks_output/`, `net_input_images/`, `net_input_masks/` — generated binary and multi-label masks.  

## Requirements

- Python 3.8+  
- Dependencies: `numpy`, `matplotlib`, `h5py`, `scikit-image`, `scipy`, `opencv-python`, `Pillow`  

## Usage

Open each notebook in sequence to reproduce the workflow:

1. Run **image normalization**.  
2. Run **probability maps post-processing** for ilastik `.h5` outputs.  
3. Run **label masks post-processing** for refined labels and dataset preparation.

---

This pipeline ensures reproducibility, cleanliness, and quality control in preparing microscopy image datasets for deep learning applications.
