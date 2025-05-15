# 🧠 Inference Evaluation of MedSAM-2 on Brain Tumor

![thumbnail](https://github.com/user-attachments/assets/f64d69d3-a156-40fc-8d31-c5e0acc451fa)
This project evaluates the inference performance of the **MedSAM-2** segmentation model on **brain tumor** datasets. It involves loading pretrained MedSAM-2 weights and applying them on brain tumor MRI scans to assess the segmentation quality visually and quantitatively.

---

## 🗂 Project Structure

- `inference-eval-of-medsam-2-on-brain-tumor.ipynb` – Main notebook for loading the model, running inference, and visualizing results.
- `images/` – (Optional) Directory to store MRI input images, corresponding ground truths & model output predictions.
- `README.md` – Project overview and instructions.

---

## 🚀 Features

- Utilizes the latest **MedSAM-2** medical segmentation model.
- Evaluates segmentation on **brain tumor** images.
- Includes visual comparison of predicted masks and ground truth.
- Supports integration with pretrained model weights.

---

## 🚀 Results

![Dataset Overview](https://github.com/user-attachments/assets/c30fe9fa-aa6c-47b3-8532-ae8a93ef0ed6)

*Fig 1: Dataset Overview (BRATS-2019)*

![Failure Analysis results](https://github.com/user-attachments/assets/70f36490-3ca7-4108-a77c-c02e40004e9f)

*Fig 2: Failure Analysis Results*

![Masked Images](https://github.com/user-attachments/assets/e267a3e8-c5a1-46c2-920f-d5e7e1783361)

*Fig 3: Masked Images of Prediction & Ground Truth*

![Slicing   Segmentation results](https://github.com/user-attachments/assets/ef79cfb6-a013-4ceb-b62c-f53f12cd30ac)

*Fig 4: Slicing & Segmentation Results*

![Unet   MedSam results comparison](https://github.com/user-attachments/assets/58f1b65b-e948-42ad-85bc-ce5250a27993)

*Fig 5: MedSAM & U-Net Comparison*

## 🧰 Requirements

Make sure to install the required dependencies before running the notebook.

```bash
pip install torch torchvision matplotlib opencv-python nibabel
```

## 🧪 How to Use

1. Download or Clone the Repository:
```bash
git clone https://github.com/yourusername/medsam2-brain-tumor-eval.git
cd medsam2-brain-tumor-eval
```
2. Download Pretrained Weights:

Get the MedSAM-2 pretrained weights (link or source should be mentioned in the notebook).

3. Prepare the Dataset:

Ensure brain tumor MRI images are placed in a structured folder (images/) or directly referenced in the notebook.

4. Run the Notebook:

Launch Jupyter Lab or Jupyter Notebook and open:
```bash
jupyter notebook inference-eval-of-medsam-2-on-brain-tumor.ipynb
```
5. View Results:

Segmentation results and evaluation metrics will be displayed within the notebook.

## 📈 Sample Output

Visual outputs include:

- Input MRI image
- Ground truth tumor mask
- MedSAM-2 predicted segmentation
- Dice coefficient

### Segmentation Performance Comparison

| Case ID               | Method          | Dice   | IoU   | Worst Slices | Spatial Consistency | Fragmentation (Pred/GT) | Notes                  |
|-----------------------|-----------------|--------|-------|--------------|---------------------|-------------------------|------------------------|
| BraTS19_2013_27_1     | MedSAM          | 0.018  | -     | -            | -                   | -                       | Complete failure       |
|                       | Simulated U-Net | 0.039  | -     | -            | -                   | -                       | 2× better than MedSAM  |
|                       | Our Method      | 0.071  | 0.037 | 114,106,107  | 17,813.42           | 18,364/2                | Best but still poor    |
| BraTS19_CBICA_AQA_1   | MedSAM          | 0.005  | -     | -            | -                   | -                       | Worst performance      |
|                       | Simulated U-Net | 0.006  | -     | -            | -                   | -                       | Minimal improvement    |
|                       | Our Method      | 0.017  | 0.009 | 106,97,98    | 44,466.45           | 18,321/16               | Extreme fragmentation |

### Key Findings

1. **Severe Underperformance**  
   - All methods show Dice scores < 0.1 (extremely poor)
   - MedSAM fails catastrophically (Dice: 0.005-0.018)

2. **Critical Issues**  
   - 🔴 **Resolution Problems**: Downsampling from 240×240→112×112 destroys details  
   - 🔴 **Fragmentation**: Predictions have 18K+ components vs GT's 2-16  
   - 🔴 **Spatial Chaos**: Consistency ratios > 17,000 indicate random predictions

3. **Method Comparison**  
   - Our method outperforms baselines but remains unacceptable  
   - U-Net shows slight advantage over MedSAM (2-3× better)

## Summary of Segmentation Performance

| Case ID               | Dice Score | IoU Score | Performance Level       |
|-----------------------|------------|-----------|-------------------------|
| BraTS19_2013_27_1     | 0.071      | 0.037     | 🟠 Poor                 |
| BraTS19_CBICA_AQA_1   | 0.017      | 0.009     | 🔴 Very Poor            |
| BraTS19_CBICA_ANZ_1   | 0.042      | 0.021     | 🟡 Marginal             |

## 📚 References

- https://colab.research.google.com/drive/1MKna9Sg9c78LNcrVyG58cQQmaePZq2k2?usp=sharing#scrollTo=FnoCVlmGIgC4
- https://github.com/bowang-lab/MedSAM2
- https://www.kaggle.com/datasets/aryashah2k/brain-tumor-segmentation-brats-2019/data

## 📄 License

This project is under the MIT License. Please check original model licenses for additional terms.

## 👨‍💻 Author
Humaima Anwar - humaimaanwar123@gmail.com
