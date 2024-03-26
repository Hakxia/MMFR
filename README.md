# MMFR
This repo is the official implementation for MMFR.


# Requirements

```bash
python==3.8.13
torch==1.8.1+cu111
torchvision==0.9.1+cu111
tensorboard==2.9.0
timm==0.3.2
scikit-learn==1.1.1
tqdm==4.64.0
numpy==1.22.4
```

# Data Preparation

### Download datasets.
#### NTU RGB+D 60 and 120
1. Request dataset here: https://rose1.ntu.edu.sg/dataset/actionRecognition
2. Download the skeleton-only datasets:
   1. `nturgbd_skeletons_s001_to_s017.zip` (NTU RGB+D 60)
   2. `nturgbd_skeletons_s018_to_s032.zip` (NTU RGB+D 120)
   3. Extract above files to `./data/nturgbd_raw`

#### PKU-MMD Phase I and Phase II
1. Request dataset here: http://39.96.165.147/Projects/PKUMMD/PKU-MMD.html
2. Download the skeleton data, label data, and the split files:
   1. `Skeleton.7z` + `Label_PKUMMD.7z` + `cross_subject.txt` + `cross_view.txt` (Phase I)
   2. `Skeleton_v2.7z` + `Label_PKUMMD_v2.7z` + `cross_subject_v2.txt` + `cross_view_v2.txt` (Phase II)
   3. Extract above files to `./data/pku_raw`

### Data Processing

#### Directory Structure

Put downloaded data into the following directory structure:

```
- data/
  - ntu/
  - ntu120/
  - nturgbd_raw/
    - nturgb+d_skeletons/     # from `nturgbd_skeletons_s001_to_s017.zip`
      ...
    - nturgb+d_skeletons120/  # from `nturgbd_skeletons_s018_to_s032.zip`
      ...
  - pku_v1/
  - pku_v2/
  - pku_raw/
    - v1/
      - label/
      - skeleton/
      - cross_subject.txt
      - cross_view.txt
    - v2/
      - label/
      - skeleton/
      - cross_subject_v2.txt
      - cross_view_v2.txt
```

#### Generating Data

- Generate NTU RGB+D 60 or NTU RGB+D 120 dataset:
```
cd ./data/ntu # or cd ./data/ntu120
# Get skeleton of each performer
python get_raw_skes_data.py
# Remove the bad skeleton 
python get_raw_denoised_data.py
# Transform the skeleton to the center of the first frame
python seq_transformation.py
```
- Generate PKU-MMD Phase I or PKU-MMD Phase II dataset:
```
cd ./data/pku_v1 # or cd ./data/pku_v2
python pku_gendata.py
```

# Training and Testing
coming soon.

# Acknowledgment
The framework of our code is based on [MAMP](https://arxiv.org/pdf/2308.07092.pdf) and [GAP](https://arxiv.org/abs/2208.05318).

Thanks to the original authors for their work!
