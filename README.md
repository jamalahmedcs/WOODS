<p align='center'>
  <img width='100%' src='./assets/banner.png' />
</p>

--------------------------------------------------------------------------------
[![Documentation Status](https://readthedocs.org/projects/mitiq/badge/?version=stable)](https://woods.readthedocs.io/en/latest)
![Continuous Integration](https://github.com/jc-audet/WOODS/actions/workflows/python-package.yml/badge.svg)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)


# Benchmarks for Out-of-Distribution Generalization in Time Series Tasks


[Understanding Rare Spurious Correlations in Neural Network](https://arxiv.org/abs/2202.05189)

Authors: [Yao-Yuan Yang](https://github.com/yangarbiter/), [Kamalika Chaudhuri](http://cseweb.ucsd.edu/~kamalika/)

# Quick Start

## Download
Some datasets require downloads in order to be used. We provide the download script to directly download our own preprocessed versions of the datasets which are ready for use. If you want to look into the preprocessing yourself, check the `fetch_and_preprocess.py` script. You can provide a specific dataset to download, or provide nothing to download all of them. See the raw and preprocessed sizes of the dataset on the dataset page of the [documentation](https://woods.readthedocs.io/en/latest/downloading_datasets.html#datasets-info).

```sh
python3 -m woods.scripts.download {dataset} \
        --data_path /path/to/data/directory
```

## Train a model
Train a model using one objective on one dataset with one test environment. For data that requires a download, you need to provide the path to the data directory with `--data_path`.

```sh
python3 -m woods.scripts.main train \
        --dataset Spurious_Fourier \
        --objective ERM \
        --test_env 0 \
        --data_path /path/to/data/directory
```

## Make a sweep
To launch a hyper parameter sweep, use the following script. Define a collection of Objective and Dataset to investigate a combination. All test environment are gonna be investigated automatically. By default, the sweep is gonna do a random search over 20 hyper parameter seeds with 3 trial seed each. For more details on the usage of the hparams_sweep, see the [documentation](https://woods.readthedocs.io/en/latest/running_a_sweep.html).

```sh
python3 -m woods.scripts.hparams_sweep \
        --dataset Spurious_Fourier TCMNIST_seq\
        --objective ERM IRM \
        --save_path ./results \
        --launcher local \
        --data_path /path/to/data/directory
```

When the sweep is complete you can compile the results in neat tables, the '--latex' argument outputs a table that can be directly copy pasted into a .tex documents. For more details on the usage of compile results, see the [documentation](https://woods.readthedocs.io/en/latest/running_a_sweep.html).

```sh
python3 -m woods.scripts.compile_results \
        --mode tables \
        --results_dir ./results \
        --latex
```

## Evaluate a model

Evaluate a single model using one objective on one dataset with one test environment.

```sh
python3 -m woods.main eval \
        --model_path /path/to/model\
        --dataset Spurious_Fourier \
        --objective ERM \
        --test_env 0
```

# Contributors
