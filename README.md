# 🍃 FreshLens AI — See Fresh. Sell Smart.

**Intelligent Fruit Quality Assessment for Smart Retail Using Deep Learning**

FreshLens AI is a computer vision system that automatically classifies fruit as **fresh or rotten** from a single image, in real time, using a lightweight deep learning model (MobileNetV2). It's built to plug into the fruit supply chain — from farm collection points and wholesale markets to retail shelves — and turn manual, inconsistent visual inspection into an instant, auditable, AI-driven decision.

---

## 🎯 The Problem

Egypt wastes an estimated **18 million tonnes of food per year** (~155 kg per person), one of the highest rates in the world (UNEP Food Waste Index Report 2024). Fruits and vegetables are the worst-performing food category globally, with loss rates climbing from 23.2% to 25.4% between 2015–2023 (FAO SDG 12.3.1). A big share of that loss happens *before* the product ever reaches a shelf — at the farm, in transport, and at wholesale — where inspection is manual, slow, and inconsistent.

## 💡 The Solution

FreshLens AI replaces manual sorting with an automated vision pipeline:

**Capture → AI Analysis (Computer Vision) → Quality Classification (Fresh / Rotten) → Business Action (Sell / Discount / Remove)**

The model inspects fruit images and returns a confidence-scored freshness verdict per item, enabling faster inspection, lower operational cost, less waste, and better product quality reaching the customer.

## 👥 Who It's For

- **Retailers & supermarkets** — automate quality checks on incoming produce and shelf stock.
- **Wholesale markets & packing houses** — catch spoilage earlier in the supply chain, where most loss occurs.
- **Exporters** — generate objective, auditable quality records for shipments (e.g. Egypt's orange exports).
- **Policy & sustainability stakeholders** — a measurable tool to support Egypt's food-waste reduction efforts.

## ✅ Value Delivered

| Benefit | Description |
|---|---|
| 🗑️ Reduce Food Waste | Detects rotten fruit early to prevent losses at every stage |
| ⚡ Faster Inspection | Automates quality checks and inspects large volumes in seconds |
| 💰 Lower Operational Cost | Minimizes manual effort and reduces sorting errors |
| ⭐ Better Customer Satisfaction | Delivers consistently higher-quality fruit |

---

## 🧠 What We Built

### Dataset
- **13,121 images** across **3 fruit categories** (Banana, Mango, Orange) × **2 quality classes** (Fresh, Rotten) = **6 classes**
- Collected under diverse real-world conditions: varying lighting, camera angles, backgrounds, fruit sizes, and spoilage patterns — improving robustness and generalization.
- Balanced class distribution, verified via exploratory data analysis (EDA), with no severe class imbalance.

### Data Pipeline
Raw Images → Label Encoding → Train/Val/Test Split (70/15/15) → RGB Conversion → Resize (224×224) → Normalization → Data Augmentation (training set only) → Shuffle → Batch → Prefetch

### Modeling Approach
Two models were trained and compared:

1. **Baseline CNN** (custom architecture) — Conv2D + BatchNorm + MaxPooling stack, GlobalAveragePooling, Dropout, Dense layers, Softmax output.
2. **MobileNetV2 (Transfer Learning)** — pretrained on ImageNet, fine-tuned for this 6-class classification task.

**Why transfer learning:** faster training (epoch time dropped from ~210s to ~70s), a lightweight footprint suited for edge/mobile deployment, and higher accuracy from less data.

### Training Configuration
- Optimizer: Adam | Learning rate: 0.001 | Batch size: 32 | Loss: Sparse Categorical Crossentropy
- Callbacks: `EarlyStopping` (patience=5), `ReduceLROnPlateau` (factor=0.2)

### Explainability
Used **Grad-CAM** to visualize which regions of the fruit the model focuses on — confirming attention concentrates on bruised/discolored areas, making decisions auditable (a manager can verify *why* an item was flagged as rotten).

---

## 📊 Results

| Metric | Baseline CNN | **MobileNetV2 (Final Model)** |
|---|---|---|
| Accuracy | 94.37% | **96.19%** |
| Precision | 94.28% | **96.22%** |
| Recall | 94.31% | **96.19%** |
| F1-Score | 94.29% | **96.19%** |
| Inference Time | 18.73 ms/image | **11.25 ms/image** |
| Model Size | 20.14 MB | **9.27 MB** |
| Error Rate (test set) | 3.81% (75/1,969 wrong) | **1.42% (28/1,969 wrong)** |

MobileNetV2 outperformed the baseline on every metric while being smaller and faster — confirming it as the better choice for real-world, in-store deployment. Most remaining errors occur between visually similar classes (e.g. rotten mango vs. rotten orange) — cases a human would also find ambiguous.

---

## 🚀 Deployment Vision

At **~10 ms per image** and a **9.27 MB** model footprint, FreshLens AI is light enough to run on edge devices (e.g. a shelf-mounted or conveyor camera) without a server-side bottleneck:

`Supermarket Camera → AI Inspection (MobileNetV2) → Quality Classification → Inventory Optimization (restock / discount / remove)`

## 🔭 What's Next

- Expand to more fruit and vegetable categories
- Mobile application for store staff
- Real-time camera integration
- Full edge AI deployment in-store

---

## 🛠️ Tech Stack
`Python` · `TensorFlow / Keras` · `MobileNetV2 (Transfer Learning)` · `Convolutional Neural Networks` · `Grad-CAM` · `NVIDIA GPU`

## 👩‍💻 Team
Haidy · Safaa · Samah · Shahinaz · Sally

---

*"See Fresh. Sell Smart."*
