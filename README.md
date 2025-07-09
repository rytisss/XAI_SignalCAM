# Lightweight Data-driven ECG Classification Approach with Explainable CAM Output
This repository contains the [PyTorch](https://pytorch.org/) implementation of the lightweight CNN-based ECG classification approach with integrated explainable AI (XAI) capabilities presented in the paper **"Lightweight Data-driven ECG Classification Approach with Explainable CAM Output"** at **The 47th Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC) 2025** by Rytis Augustauskas, Ana Santos Rodrigues, Daivaras Sokas, Otilia Bularca, and Vaidotas Marozas.
### High-level overview
This repository describes data wrangling for the [PTBXL](https://physionet.org/content/ptb-xl/1.0.3/) dataset and binary classification problem, where the data is separated into 2 classes **NORMAL** and **ABNORMAL**. While the current implementation is designed for binary classification with integrated explainability in a single iteration, the approach is also adaptable to multiclass classification tasks and supports different CNN architectures. The codebase includes the full workflow:
- Data loading and overview
- Dataset splitting and preprocessing (with optional augmentation)
- Model training and evaluation
- Explainability analysis and visualization
<div align="center">
<img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/research_codebase/res/demo_xai_size_reduced.gif" width="600"/>
</div> 

### Data processing  
The code implements all essential steps for signal preprocessing and augmentation, following the structure of the provided pipeline:
<div align="center">
<img src="https://github.com/rytisss/XAI_SignalCAM/blob/main/res/Pipeline.png" width="150"/>
</div>  
Scaling (standardization) transforms the signal into the range [−1,1] according to the following expression:  
<div align="center">
<img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/processing_explanation/res/standartidization_formula.jpg" width="300"/>
</div>  

Where:  
- `X_d` – detrended input signal  
- `median(X_d)` – median of the detrended signal  
- `X_st` – standardized signal

<p align="center">
  <table>
    <tr>
      <td align="center">
        <img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/processing_explanation/res/orig_val.png" width="400"/>
        <br><b>Original Signal</b>
      </td>
      <td align="center">
        <img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/processing_explanation/res/detrend_valid.png" width="400"/>
        <br><b>Detrended Signal</b>
      </td>
    </tr>
    <tr>
      <td align="center">
        <img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/processing_explanation/res/scaled_valid.png" width="400"/>
        <br><b>Scaled Signal</b>
      </td>
      <td align="center">
        <img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/processing_explanation/res/augmentation.png" width="400"/>
        <br><b>Augmentation Pipeline (Sample)</b>
      </td>
    </tr>
  </table>
</p>

### Integrated explainability idea
- This work adapts a class activation map (CAM)-based explainability technique, designed for 1D time-series ECG signals. The method enhances model interpretability by identifying which parts of the input signal most influenced the prediction.  
- A non-trainable CAM output layer is added after the global average pooling layer. It computes feature importance by taking the dot product of the latent feature maps and the output layer weights. The result is a single explainability heatmap aligned with the input signal, rescaled to match its original length and normalized to the [0, 1] range.  
- The explainability output is generated post-training and does not affect model parameters. In binary classification, one CAM map is produced. For multiclass problems, separate maps can be created per class. Importantly, this addition increases computational complexity by only ~15% while maintaining the same number of parameters (on the presented architecture).  
<div align="center">
<img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/research_codebase/res/xai_branch.png" width="300"/>
</div>

### Quick start (installation)

1. Clone repository:<br />
```
git clone https://github.com/rytisss/XAI_SignalCAM.git
cd XAI_SignalCAM
```

2. Execute the line in the terminal to set up the environment (install 3rdParties):<br />
```
pip install -r requirements.txt
```

3. Open **Jupyter**:
```
jupyter notebook
```

4. Launch [ptbxl_data_classification.ipynb](https://github.com/rytisss/XAI_SignalCAM/blob/feature/research_codebase/ptbxl_data_classification.ipynb)!


## Content overview

https://github.com/user-attachments/assets/017bd275-c3de-4b07-b89b-71a95e354773

## Citation (will be updated) 
```
@inproceedings{augustauskas2025lightweight,
  title={Lightweight Data-driven ECG Classification Approach with Explainable CAM Output},
  author={Augustauskas, Rytis and Rodrigues, Ana Santos and Sokas, Daivaras and Bularca, Otilia and Marozas, Vaidotas},
  booktitle={2025 47th Annual International Conference of the IEEE Engineering in Medicine and Biology Society (EMBC)},
  year={2025},
  organization={IEEE}
}
```

## Aknowledgement  
This research was supported by the [CVDLINK](https://cvdlink-project.eu/) project (EU Horizon grant agreement N°101137278)
<div align="center">
<img src="https://github.com/rytisss/XAI_SignalCAM/blob/feature/research_codebase/res/CVDLINK_logo-v.png" width="450"/>
</div>
