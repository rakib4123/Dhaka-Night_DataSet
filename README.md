# DhakaNight Dataset

A night-time traffic dataset from the streets of Dhaka, Bangladesh, for training and benchmarking **object detection under low light**.

> 📄 Introduced in *DhakaNight: A Benchmark for Low-Light Object Detection in Dense Urban Night Traffic* — presented at **ICCA 2026** (in cooperation with ACM).
>
> 🧪 Training and evaluation code: [rakib4123/Dhaka_Night](https://github.com/rakib4123/Dhaka_Night)

## At a glance

| | |
| --- | --- |
| Images | **2,380** night-time street images, 640 × 640 JPG |
| Annotations | **45,224** bounding boxes, manually annotated (YOLO format) |
| Classes | **10** |
| Splits | train 1,538 · val 233 · test 609 |

## Classes

Includes vehicle types specific to Dhaka's roads, such as CNGs (auto-rickshaws), cycle rickshaws and human haulers.

| ID | Class | train | val | test | Total |
| --- | --- | ---: | ---: | ---: | ---: |
| 0 | bicycle | 134 | 14 | 165 | 313 |
| 1 | bus | 4,397 | 96 | 913 | 5,406 |
| 2 | car | 9,101 | 559 | 3,005 | 12,665 |
| 3 | cng | 4,116 | 124 | 1,071 | 5,311 |
| 4 | human_hauler | 10 | 0 | 83 | 93 |
| 5 | motorcycle | 5,948 | 197 | 1,619 | 7,764 |
| 6 | pedestrian | 2,237 | 163 | 3,686 | 6,086 |
| 7 | pickup_van | 580 | 47 | 199 | 826 |
| 8 | rickshaw | 2,245 | 112 | 2,783 | 5,140 |
| 9 | truck | 1,334 | 45 | 241 | 1,620 |
| | **Total** | **30,102** | **1,357** | **13,765** | **45,224** |

`bicycle` and `human_hauler` are rare, and `human_hauler` has no validation examples, so expect per-class scores for those two to be noisy.

## Structure

```
Dhaka-Night_DataSet/
├── data.yaml
├── train/
│   ├── images/   dn_XXXX.jpg
│   └── labels/   dn_XXXX.txt
├── val/
│   ├── images/
│   └── labels/
└── test/
    ├── images/
    └── labels/
```

Each label file has one line per object in standard YOLO format:

```
<class_id> <x_center> <y_center> <width> <height>     # all values normalised to 0–1
```

## Quick start (Ultralytics YOLOv8)

```bash
git clone https://github.com/rakib4123/Dhaka-Night_DataSet.git
pip install ultralytics
yolo detect train data=Dhaka-Night_DataSet/data.yaml model=yolov8n.pt epochs=100 imgsz=640 batch=16
```

The split paths in `data.yaml` are relative to the dataset folder, so it works from wherever you clone it.

## Baseline results

From the paper, on the 609-image test split:

| Model | Pre-processing | mAP@0.5 | mAP@0.5:0.95 |
| --- | --- | --- | --- |
| YOLOv8n | none | 0.587 | 0.401 |
| YOLOv8s | none | **0.610** | **0.417** |
| YOLOv8n | best enhancement (Gamma) | 0.591 | 0.403 |

Full comparison, including CLAHE, Zero-DCE and RetinexFormer, and a per-illumination breakdown: see the [training repo](https://github.com/rakib4123/Dhaka_Night).

## Citation

If you use this dataset, please cite the paper:

> Md. Rakib Hossain et al. *DhakaNight: A Benchmark for Low-Light Object Detection in Dense Urban Night Traffic.* 4th International Conference on Computing Advancements (ICCA 2026), Dhaka, Bangladesh.

## Usage and contact

No open-source license has been attached to this dataset yet. Please get in touch before using it beyond research and evaluation.

**Md. Rakib Hossain** — [LinkedIn](https://www.linkedin.com/in/md-rakib-hossain-519818263) · [Portfolio](https://rakib4123.github.io)
