# Occlusion Analysis and Filter Visualization

An exploration of CNN interpretability techniques using pretrained models (VGG16 and AlexNet) on ImageNet data. This project implements **occlusion sensitivity analysis** to identify which image regions drive classification decisions, and **convolutional filter visualization** to understand what features CNN layers learn.

## Background

Deep convolutional neural networks achieve high accuracy on image classification tasks, but their internal decision-making process is largely opaque. Two complementary techniques help shed light on what these models learn:

- **Occlusion Sensitivity Analysis** — Systematically occlude regions of an input image with a gray patch and observe how the model's predicted probability changes. Regions where occlusion causes the largest probability drop are the most important for the classification. The result is a heatmap that highlights discriminative image regions.

- **Filter Visualization** — Directly inspect the learned convolutional filter weights. Since convolution is analogous to a dot product, filters respond most strongly to input patterns that align with their weights. Visualizing filters reveals the low-level features (edges, textures, colors) and higher-level patterns the network has learned to detect.

## Methodology

### Occlusion Analysis
1. Load a pretrained **VGG16** model and a set of ImageNet images (dome, harmonica, stethoscope).
2. For each image, slide a gray occlusion patch (size 32, stride 14) across all spatial positions.
3. At each position, record the softmax probability for the true class.
4. Construct a heatmap: darker regions indicate where occlusion caused the largest probability drop, revealing the most important features for classification.

### Filter Visualization
1. Load a pretrained **AlexNet** model.
2. Extract convolutional filter weights from layers at different depths (layers 0, 3, 6).
3. Visualize filters in three modes:
   - **Multi-channel (RGB)** — First-layer filters shown as color images, revealing edge and color detectors.
   - **Single-channel** — Individual filter channels displayed separately.
   - **Collated** — All filter channels tiled into a single heatmap for a compact overview.
4. Compare filters across layers to observe the progression from simple edge detectors (early layers) to more complex texture/pattern detectors (deeper layers).

## Results

- The occlusion heatmap clearly highlights the semantically meaningful region of the input image (e.g., the dome structure, harmonica keys), confirming that VGG16 focuses on the correct object rather than background context.
- First-layer AlexNet filters show recognizable Gabor-like edge detectors and color-opponent filters, consistent with known findings in the literature.
- Deeper-layer filters become increasingly abstract and harder to interpret visually, reflecting the hierarchical feature learning in CNNs.

## Repository Structure

```
.
├── Occlusion_Analysis_and_Filter_Visualization.ipynb   # Main notebook
├── data.zip                                            # ImageNet sample images
├── requirements.txt                                    # Python dependencies
├── .gitignore
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.7+
- (Optional) CUDA-enabled GPU for faster inference

### Installation

```bash
git clone https://github.com/<your-username>/Occlusion-Analysis-and-Filter-Visualization.git
cd Occlusion-Analysis-and-Filter-Visualization
pip install -r requirements.txt
```

### Running

Open the notebook and run all cells:

```bash
jupyter notebook Occlusion_Analysis_and_Filter_Visualization.ipynb
```

The notebook will automatically extract `data.zip` and download pretrained model weights on first run.

## References

- Zeiler, M. D., & Fergus, R. (2014). *Visualizing and Understanding Convolutional Networks.* ECCV 2014.
- Simonyan, K., & Zisserman, A. (2015). *Very Deep Convolutional Networks for Large-Scale Image Recognition.* ICLR 2015.
- Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012). *ImageNet Classification with Deep Convolutional Neural Networks.* NeurIPS 2012.
