# README

## Project Overview
Welcome to the `embedding-to-individual-id` project. This repository contains a deep learning pipeline to identify individual birds using embeddings extracted from **BirdNET** and **Google Perch**. It supports training and evaluation of **FCNN** (Fully Connected Neural Networks) and **RNN** (Recurrent Neural Networks), specifically with LSTM.

## Features
- **Modular Architecture**: Easy to adapt to new species or embedding types.
- **Multi-Model Support**: Compare performance between FCNN and LSTM.
- **Streamlined Workflow**: From raw embeddings to performance metrics and confusion matrices.

## Getting Started

### 1. Prerequisites
Install [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/).

### 2. Installation
Clone the repository and navigate to the project directory:
```bash
git clone xxxxx
cd xxxxx
```

### 3. Environment Setup
Create the environment using the provided YAML file:
   ```bash
   conda env create -f environment.yml
   conda activate embtoindv
   ```


## Data & Inputs
This repository requires embeddings as input. You can generate them using the [Extraction Repository] or download the pre-extracted datasets:

### 1 Embeddings
Access the pre-extracted embeddings here:

[Datasets - Zenodo](https://doi.org/10.5281/zenodo.18603176) 

Organization: Place all embeddings inside the Output_files folder in the project root, separating them by window duration (3s or 5s):

```
Output_files/
├── Embeddings_from_3sPadding/
│    ├── <dataset_name>_parquet_parts/    # .parquet files (e.g., littleowl_parquet_parts)
|    └── ...
└── Embeddings_from_5sPadding/
     ├── <dataset_name>_parquet_parts/    # .parquet files (e.g., littleowl_parquet_parts)
     └── ...
```

### 2. Metadata
Metadata files are not included in this repository. Access them through:

[Metadata - Zenodo](https://doi.org/10.5281/zenodo.18603176)

Paste the files into the `Output_metadata` folder following this structure:


```
Output_metadata
├── GreatTit_metadata
│   ├── final_greatTit_metadata.csv
│   └── ... (train, test, val csv files)
├── chiffchaff-fg
├── KiwiTrimmed
├── littleowl-fg
├── littlepenguin_metadata
├── pipit-fg
└── rtbc_metadata
```


### 3. Project Structure & Workflow
The notebooks are categorized by architecture and dataset:

- FCNN Models: Found in Notebooks/. High-performance classification using 1024-D (BirdNET) or 1280-D (Perch) features.

- Pooling Strategies: Notebooks with _pooling in the name. They explore global average or maximum pooling across multiple temporal segments.

- LSTM Models: Specialized notebooks for capturing temporal dependencies within vocalization sequences.



Study Cases
Includes experiments for both Across-year and Within-year temporal constraints across all target species.


## How to Run
1. Verify Data: Ensure .parquet files and .csv metadata are in their respective Output_ folders.

2. Select a Model: Open a notebook from the Notebooks/ directory (e.g., Notebooks/chiffchaff_withinyear_LSTM_birdnet.ipynb).

Configure Paths: Verify the data paths in the initial cells match your local directory structure.

Train and Evaluate: Execute all cells. The notebooks will output accuracy metrics, loss curves, and confusion matrices for the test split.

## Model Details
- Input: BirdNET v2.4 (1024-D) or Google Perch (1280-D) embeddings.
- FCNN: Dense layers with Dropout and Batch Normalization.
- RNN: LSTM-based architecture for sequence processing.

Note: This repository focuses on the classification and inference stage. For audio preprocessing and raw embedding extraction, please refer to the Extraction Repository.

## Contributing
We welcome contributions! 

## License
This project is licensed under the [MIT License](LICENSE).
