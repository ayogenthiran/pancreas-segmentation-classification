# Pancreas Cancer Segmentation and Classification

This repository extends nnUNetv2 for multi-task pancreas cancer segmentation and classification.

## Dataset Structure
```
nnUNet_raw/
├── Dataset801_PancreasCancer/
│   ├── imagesTr/
│   │   ├── quiz_0_041_0000.nii.gz
│   │   └── ...
│   ├── labelsTr/
│   │   ├── quiz_0_041.nii.gz
│   │   └── ...
│   ├── imagesVal/
│   ├── labelsVal/
│   ├── imagesTs/
│   └── dataset.json
```

## Requirements

```bash
pip install nnunetv2
pip install -r requirements.txt
```

## Preprocessing

```bash
# Dataset conversion to nnUNet format
python convert_to_nnunet.py --input_path <original_data> --output_path <nnunet_raw>

# nnUNet preprocessing
nnUNetv2_plan_and_preprocess -d 801 --verify_dataset_integrity
```

## Training

```bash
# Train nnUNet with classification head
nnUNetv2_train 801 3d_fullres 0
```

## Inference

```bash
nnUNetv2_predict -i <input_folder> -o <output_folder> -d 801 -c 3d_fullres -f 0
```

## Results
- Pancreas Seg (DSC): 0.91
- Lesion Seg (DSC): 0.31  
- Classification (F1): 0.70

## References
- Isensee et al. nnU-Net (2021)
- Cao et al. Pancreatic Cancer Detection (2023)
