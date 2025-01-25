# Pancreas Cancer Segmentation and Classification

This repository extends nnUNetv2 for multi-task pancreas cancer segmentation and classification.

## Dataset Structure
```
nnUNet_raw/
├── Dataset801_PancreasCancer/
│   ├── imagesTr/
│   │   ├── quiz_0_041_0000.nii.gz  
│   │   ├── quiz_1_042_0000.nii.gz  
│   │   ├── quiz_2_043_0000.nii.gz
│   │   └── ...
│   ├── labelsTr/
│   │   ├── quiz_0_041.nii.gz
│   │   ├── quiz_1_042.nii.gz
│   │   ├── quiz_2_043.nii.gz
│   │   └── ...
│   ├── imagesVal/
│   ├── labelsVal/
│   ├── imagesTs/
│   ├── dataset.json
│   └── subtype_mapping.json  # Maps case IDs to subtypes (0,1,2)
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
- Isensee, F., Jaeger, P.F., Kohl, S.A.A. et al. nnU-Net: a self-configuring method for deep learning-based biomedical image segmentation. *Nat Methods* 18, 203–211 (2021). https://doi.org/10.1038/s41592-020-01008-z

- Cao, K., Xia, Y., Yao, J. et al. Large-scale pancreatic cancer detection via non-contrast CT and deep learning. *Nat Med* 29, 3033–3043 (2023). https://doi.org/10.1038/s41591-023-02640-w

- Maier-Hein, L., Reinke, A., Godau, P. et al. Metrics reloaded: recommendations for image analysis validation. *Nat Methods* 21, 195–212 (2024). https://doi.org/10.1038/s41592-023-02151-z

- Hu, Y., et al. Rapid and Accurate Diagnosis of Acute Aortic Syndrome using Non-contrast CT: A Large-scale, Retrospective, Multi-center and AI-based Study. *arXiv preprint* arXiv:2406.15222 (2024). https://arxiv.org/abs/2406.15222

- Fast and Low-resource Semi-supervised Abdominal Organ Segmentation in CT. *FLARE 2022 Challenge*. Retrieved from https://flare22.grand-challenge.org/awards/

- Fast, Low-resource, and Accurate Organ and Pan-cancer Segmentation in Abdomen CT. *AbdomenCT-Org Challenge 2023*. Retrieved from https://codalab.lisn.upsaclay.fr/competitions/12239#learn_the_details-awards
