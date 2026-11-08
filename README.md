# AI-Based Plant Root Analysis

Automated plant root segmentation and root-length measurement from images, using deep learning and computer vision.

Developed during a research internship at the **Indian Institute of Technology (IIT) Bhubaneswar** (May 2026 – July 2026).

---

## Overview

Measuring root traits by hand is slow and subjective. This project provides an end-to-end pipeline that:

1. Takes a plant root image as input.
2. Segments the root system with a **UNet++** model using an **EfficientNet-B4** encoder, implemented in **PyTorch**.
3. Post-processes the predicted mask to estimate:
   - **Total Root Length (TRL)**: the combined length of all roots in the image.
   - **Primary Root Length (PRL)**: the length of the main (primary) root.

## Pipeline

```
Root image ──► Pre-processing ──► UNet++ (EfficientNet-B4) ──► Binary root mask
                                                                     │
                                          Skeletonization / length estimation
                                                                     │
                                                          TRL and PRL outputs
```

## Dataset

The data is organised into three parts:

| Folder | Contents |
|---|---|
| `images/` | Raw root images (model input) |
| `mask/` | Ground-truth segmentation masks (training targets) |
| `rsml/` | Root System Markup Language (RSML) annotations, used as reference root structure and length |

> The archives are large (the image set is several hundred MB), so they are not stored in this repository. Download them separately and extract them as shown below.

<!-- TODO: add dataset source / link, number of images, image resolution, and train/val/test split -->

## Repository Structure

```
.
├── Root_Analysis_Fixed.ipynb   # Main notebook: data loading, training, evaluation, TRL/PRL estimation
├── src/                        # Supporting source code
├── data/
│   ├── images/                 # extracted from the images archive
│   ├── mask/                   # extracted from the mask archive
│   └── rsml/                   # extracted from the rsml archive
└── README.md
```

<!-- TODO: list the individual files inside src/ with one line each -->

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Soumyditya/<repo-name>.git
cd <repo-name>
```

### 2. Install dependencies

```bash
pip install torch torchvision segmentation-models-pytorch opencv-python numpy matplotlib scikit-image jupyter
```

> Check this list against the imports at the top of `Root_Analysis_Fixed.ipynb` and add or remove packages to match.

### 3. Prepare the data

Extract the archives into a `data/` folder so that the layout matches the structure above:

```bash
mkdir -p data/images data/mask data/rsml
unzip images-*.zip -d data/images
unzip mask-*.zip   -d data/mask
unzip rsml-*.zip   -d data/rsml
unzip src-*.zip    -d src
```

### 4. Run the notebook

```bash
jupyter notebook Root_Analysis_Fixed.ipynb
```

Update the dataset paths in the first cells if your folders are named differently, then run the cells in order.

## Model

| Component | Choice |
|---|---|
| Architecture | UNet++ |
| Encoder | EfficientNet-B4 |
| Framework | PyTorch |
| Task | Binary semantic segmentation (root vs. background) |

<!-- TODO: add loss function, optimizer, learning rate, batch size, epochs, input size, augmentations -->

## Measurements

- **TRL (Total Root Length):** predicted mask is skeletonized, and the skeleton length in pixels is converted to physical units using the image scale.
- **PRL (Primary Root Length):** length of the longest connected path along the skeleton, corresponding to the primary root.

<!-- TODO: confirm the exact method used in the notebook and the pixel-to-mm scale -->

## Results

<!-- TODO: replace with your real numbers -->

| Metric | Value |
|---|---|
| Dice / F1 | _add_ |
| IoU | _add_ |
| TRL error vs. RSML reference | _add_ |
| PRL error vs. RSML reference | _add_ |

Add a few sample images here (input, predicted mask, overlay) for a quick visual summary.

## Tech Stack

Python, PyTorch, UNet++, EfficientNet-B4, OpenCV, NumPy, Jupyter Notebook

## Author

**Soumyaditya Majhi**
B.Tech Computer Science, XIM University
[LinkedIn](https://linkedin.com/soumyaditya-majhi-439792295) · [GitHub](https://github.com/Soumyditya)

## Acknowledgements

Research internship at the Indian Institute of Technology (IIT) Bhubaneswar.
