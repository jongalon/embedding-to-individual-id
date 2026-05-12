# README

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18603176.svg)](https://doi.org/10.5281/zenodo.18603176)

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

[Datasets - Zenodo](https://doi.org/10.5281/zenodo.18603175) 

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
The repository uses a small set of general notebooks rather than separate notebooks for each dataset and architecture. The main notebooks are located in the `Notebooks/` directory:

- `Template_LSTM_birdnet.ipynb`: main notebook for the BirdNET + LSTM experiments. It supports ordered and shuffled embedding sequences through the configuration block.
- `Template_FCNN_birdnet_and_perch_onset_gap.ipynb`: main notebook for the FCNN baseline experiments. It supports BirdNET and Perch embeddings, as well as onset and global average pooling configurations.
- `Summary metrics LSTM.ipynb`: notebook for summarizing LSTM results across datasets, splits, seeds, and sequence-order conditions.
- `Summary metrics onset gap.ipynb`: notebook for summarizing FCNN onset and GAP baseline results.
- `02_runtime_benchmark_lstm_inference_cpu.ipynb`: notebook for CPU runtime benchmarking of the BirdNET + LSTM inference pipeline.
- `Per_individual_analysis_kiwi.ipynb`: notebook for per-individual analysis of the great spotted kiwi experiment.

Study cases include experiments under within-year and across-year temporal settings, depending on the available metadata for each species. Dataset, split type, embedding backbone, pooling strategy, and ordered or shuffled sequence mode are selected inside the corresponding notebook configuration cells.

## How to Run
1. Verify the data structure. Ensure that the `.parquet` embedding files and `.csv` metadata files are placed in the corresponding `Output_files/` and `Output_metadata/` folders.

2. Select the appropriate notebook from the `Notebooks/` directory. For LSTM experiments, open:

```bash
Notebooks/Template_LSTM_birdnet.ipynb
```

For FCNN onset and GAP baseline experiments with BirdNET or Perch embeddings, open:

```bash
Notebooks/Template_FCNN_birdnet_and_perch_onset_gap.ipynb
```

3. Configure the experiment in the initial cells. Set the dataset name, split type, random seed, input paths, output paths, and experiment-specific options, such as ordered or shuffled sequences for the LSTM notebook, or backbone and pooling strategy for the FCNN notebook.

4. Run all cells. The notebooks train the selected model, evaluate it on the test split, and save the resulting metrics and reports in the configured output folders.

## Model Details
- Input: BirdNET v2.4 (1024-D) or Google Perch (1280-D) embeddings.
- FCNN: Dense neural network baseline applied to onset embeddings or pooled embedding representations.
- LSTM: BirdNET-based recurrent architecture for processing sequences of window-level embeddings. The LSTM workflow supports ordered sequences and shuffled-sequence ablations.

Note: This repository focuses on the classification and inference stage. For audio preprocessing and raw embedding extraction, please refer to the Extraction Repository.

## Contributing
We welcome contributions! 

## License
This project is licensed under the [MIT License](LICENSE).
