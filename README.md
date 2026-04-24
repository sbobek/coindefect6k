# CoinDefect6k


## Content

This repository contains two notebooks for working with the public defect datasets:

- [prodicoin_freeze_dataset_analysis.ipynb](prodicoin_freeze_dataset_analysis.ipynb): indexes the dataset folders, summarizes class and defect distributions, and generates quick plots and sample grids.
- [prodicoin_freeze_dataset_benchmark_anomalib.ipynb](prodicoin_freeze_dataset_benchmark_anomalib.ipynb): runs Anomalib benchmark experiments on the folder-based datasets and saves the results to CSV files.


## Installation

To run benchmarks you will also need `torch` prefferably with CUDA support.
Make sure to install the correct version of PyTorch for your CUDA version. Do not adjust 'cu118' if you have a different CUDA version - this version is required for all benchmarks to run without errors.
Because of the fact that benchrmark relies on anomalib which is extensively developped, make sure your verisos of python and other packages matches these in `requirements.txt`:

```
conda create -n coindefect6k python=3.10.11
conda activate coindefect6k
conda install pip
pip install torch==2.3.1 torchvision==0.18.1 torchaudio==2.3.1 --index-url https://download.pytorch.org/whl/cu118
```

After that, run other requirements install
```
pip install -r requirements.txt
```

## Data and directory struucture

It is assumed that the notebooks are locate in the folder that contains datasets obtained from Zenodo, and have following structure.
**Note that the `dataset_public_manufacturing_defects` is nesten in another `dataset_public_manufacturing_defects`** and similarly in the circulating defects version.

For manufacturing defects:
```
dataset_public_manufacturing_defects
└── dataset_public_manufacturing_defects
    ├── test
    │   ├── bad
    │   └── good
    └── train
        └── good
```

For circulation defects:
```
dataset_public_circulation_quality
└── dataset_public_circulation_quality
    ├── test
    │   ├── bad
    │   └── good
    └── train
        └── good
```

The easiest way to achieve this is to execute following:

```
git clone https://github.com/sbobek/coindefect6k
cd coindefect6k

set -euo pipefail

wget -O dataset_public_circulation_quality.zip "https://zenodo.org/api/records/18773634/files/dataset_public_circulation_quality.zip/content"
wget -O dataset_public_manufacturing_defects.zip "https://zenodo.org/api/records/18773634/files/dataset_public_manufacturing_defects.zip/content"

mkdir -p dataset_public_circulation_quality dataset_public_manufacturing_defects

unzip -q dataset_public_circulation_quality.zip -d dataset_public_circulation_quality
unzip -q dataset_public_manufacturing_defects.zip -d dataset_public_manufacturing_defects

```