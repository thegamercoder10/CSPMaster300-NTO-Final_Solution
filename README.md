# NTO Final 2021-2022 - Team CSPMaster300 Solution

This repository contains the final solution by team **CSPMaster300** for the [NTO Final 21-22](https://ods.ai/competitions/nto_final_21-22) competition.

🏆 **Result:** 16th place out of 42 teams. Overall Finalists.
📈 **Final CER:** `0.2222454791`

## Competition Overview

The competition focused on Optical Character Recognition (OCR) and text segmentation in school notebooks. 

The evaluation metric used was a modified Character Error Rate (CER). It matches predicted text polygons with ground truth polygons using Intersection over Union (IoU > 0). The CER is then calculated as the sum of Levenshtein distances between the predicted and true strings, divided by the total length of the true strings.

## Solution Architecture

Our pipeline consists of two main stages:
1. **Text Segmentation:** A Detectron2 (Mask R-CNN) model extracts text line polygons from images.
2. **Optical Character Recognition (OCR):** A custom CRNN model with a ConvNeXt/ResNet-34 backbone and BiLSTM, trained with CTC Loss, predicts the text within each extracted polygon.

## Project Structure

```text
.
├── inference/
│   ├── run.py                        # Full inference pipeline combining segmentation and OCR
│   ├── model_final.pth               # Trained Detectron2 segmentation model weights
│   └── ocr-model-last.ckpt           # Trained CRNN OCR model weights
├── segmentation_training.ipynb       # Detectron2 Mask R-CNN training notebook
└── ocr_training.ipynb                # CRNN + CTC Loss training notebook
```

## How to Run Inference

The `inference/run.py` script runs the end-to-end pipeline. It expects a directory of images and an output path for the JSON results.

```bash
cd inference
python run.py <TEST_IMAGES_PATH> <SAVE_PATH.json>
```

The script will read all images from `<TEST_IMAGES_PATH>`, run segmentation to find text polygons, crop them, run the OCR model to extract text, and save the predictions to `<SAVE_PATH.json>`.

## Training

- **Segmentation:** Open `segmentation_training.ipynb` to see the Detectron2 setup and training routine. We utilized the `COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x` architecture.
- **OCR:** Open `ocr_training.ipynb` to see the CRNN setup, data augmentations, and training routine.

## Team

**CSPMaster300**
- Finalists in the NTO Final 21-22 competition.
