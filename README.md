# Vision-Guided Jersey Number Recognition

**A Pose-Aware Torso Localization and Multi-Variant OCR Pipeline for Football Player Identification in Images and Broadcast Video**

Undergraduate thesis project — Dept. of Computer Science & Engineering, Premier University, Chattogram

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-DL-orange)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Overview

This project addresses **jersey number recognition** in football — one of the most reliable visual cues for player identification — using two complementary deep-learning pipelines:

1. **Image Pipeline** — pose-guided torso localization followed by a legibility check and multi-variant OCR, for identifying jersey numbers in single football images.
2. **Video Pipeline** — a tracking-based pipeline for broadcast football video that combines detection, multi-object tracking, and temporal consensus to resolve jersey numbers across frames.

Both pipelines are evaluated on the **SoccerNet SN-Jersey 2023** dataset, with the video pipeline additionally evaluated against manually annotated ground truth using standard multi-object-tracking metrics.

## Authors

| Role | Name |
|---|---|
| Author | Julkarnine Tarek — [GitHub](https://github.com/julkarnine3) · [LinkedIn](https://linkedin.com/in/julkarninetarek/) |
| Author | Muhammad Nayeemul Hasan Chy |
| Supervisor | Tamim Hossain, Lecturer, Dept. of CSE, Premier University Chattogram |

## Architecture

### Image Pipeline
Detection → Pose-guided torso localization → Legibility classification (ResNet-18) → Multi-variant OCR

### Video Pipeline
Detection → Multi-object tracking (ByteTrack) → Per-track OCR (PERSeq, primary; EasyOCR, fallback) → Temporal consensus across frames

> Pipeline diagrams are available in [`docs/diagrams/`](docs/diagrams/).

## Repository Structure

```
pose_aware_jersey_number_recognition/
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── docs/
│   ├── report/                 # Final thesis report (PDF) + LaTeX source
│   └── diagrams/                # Architecture / flowchart figures (SVG, PNG, PDF)
├── notebooks/
│   ├── image_pipeline.ipynb
│   └── video_pipeline.ipynb     # sn_je_vid_v2.ipynb
├── annotations/                  # CVAT-exported ground-truth CSVs (small files only)
└── results/
    ├── figures/
    └── metrics/
```

## Dataset

This project uses the **SoccerNet SN-Jersey 2023** dataset. The raw dataset is **not included** in this repository due to size and license terms — see [SoccerNet](https://www.soccer-net.org/) for access instructions. Only derived, lightweight annotation files (ground-truth CSVs exported from CVAT) are versioned here.

## Installation

```bash
git clone https://github.com/hossain-tamim/pose_aware_jersey_number_recognition.git
cd pose_aware_jersey_number_recognition
pip install -r requirements.txt
```

Notebooks auto-detect the runtime environment (Google Colab / Kaggle / local).

## Usage

```bash
# Image pipeline
jupyter notebook notebooks/image_pipeline.ipynb

# Video pipeline
jupyter notebook notebooks/video_pipeline.ipynb
```

## Evaluation

Video-pipeline tracking quality is measured with standard MOT metrics (MOTA, MOTP, IDF1, via `motmetrics`), and jersey number accuracy is scored using majority-overlap track voting against manually annotated (CVAT) ground truth.

| Metric | Score |
|---|---|
| Image-pipeline test-accuracy | _80%_ |
| Video-pipeline (RAW) | _67.15%_ |
| Video-pipeline (temporal_voting) | _84.53%_ |
| Jersey number accuracy (video gt_eval) | _74.78%_ |

## Report

The full thesis report is available at [`docs/report/`](docs/report/).

## Acknowledgments

This work made use of AI-assisted and annotation tools including ChatGPT, Claude, and CVAT, in accordance with departmental academic policy.

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.
