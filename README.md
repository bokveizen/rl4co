<div align="center">

# RL4CO

<a href="https://pytorch.org/get-started/locally/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-ee4c2c?logo=pytorch&logoColor=white"></a>
<a href="https://pytorchlightning.ai/"><img alt="Lightning" src="https://img.shields.io/badge/-Lightning-792ee5?logo=pytorchlightning&logoColor=white"></a><a href="https://github.com/pytorch/rl"><img alt="base: TorchRL" src="https://img.shields.io/badge/base-TorchRL-red">
<a href="https://hydra.cc/"><img alt="config: Hydra" src="https://img.shields.io/badge/config-Hydra-89b8cd"></a> [![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)![license](https://img.shields.io/badge/license-Apache%202.0-green.svg?)
<!-- ![testing](https://github.com/kaist-silab/ncobench/actions/workflows/tests.yml/badge.svg) -->

[[Notion Page]](https://www.notion.so/kaistsilab/RL4CO-NIPS-23-f9b2e557d6834739a776f595453bae0d?pvs=4) [[Sofware Practices]](https://www.notion.so/kaistsilab/Software-929d1248c13a4cb0911d317311787f3e?pvs=4)
</div>



## Description

Code repository for RL4CO. Based on [TorchRL](https://github.com/pytorch/rl) and the [Lightning-Hydra-Template](https://github.com/ashleve/lightning-hydra-template) best practices.


## How to run

Colone project and install dependencies:

```bash
git clone https://github.com/kaist-silab/rl4co && cd rl4co
pip install light-the-torch && python3 -m light_the_torch install --upgrade -r requirements.txt
```
The above script will [automatically install](https://github.com/pmeier/light-the-torch) PyTorch with the right GPU version for your system. Alternatively, you can use `pip install -r requirements.txt`. Alternatively, you can install the package locally with `pip install -e .`.


Train model with default configuration (AM on TSP environment):
```bash
python run.py  
```

Train model with chosen experiment configuration from [configs/experiment/](configs/experiment/)

```bash
# Change experiment (e.g. tsp/am, and environment with 42 cities)
python run.py experiment=tsp/am env.num_loc=42    

# Disable logging
python run.py experiment=tsp/am logger='null'

# Create a sweep over hyperparameters (-m for multirun)
python run.py -m experiment=tsp/am  train.optimizer.lr=1e-3,1e-4,1e-5

```

### Testing

Run tests with `pytest`:

```bash
pytest tests/test_*.py
```
We will enable automated tests when we make the repo public.


## Project structure
> Note: general layout, may be subject to change

```

├── .github                   <- Github Actions workflows
│
├── configs                   <- Hydra configs
│   ├── callbacks                <- Callbacks configs
│   ├── data                     <- Data configs
│   ├── debug                    <- Debugging configs
│   ├── experiment               <- Experiment configs
│   ├── extras                   <- Extra utilities configs
│   ├── hparams_search           <- Hyperparameter search configs
│   ├── hydra                    <- Hydra configs
│   ├── local                    <- Local configs
│   ├── logger                   <- Logger configs
│   ├── model                    <- Model configs
│   ├── paths                    <- Project paths configs
│   ├── trainer                  <- Trainer configs
│   │
│   ├── eval.yaml             <- Main config for evaluation
│   └── train.yaml            <- Main config for training
│
├── data                   <- Project data
│
├── logs                   <- Logs generated by hydra and lightning loggers
│
├── notebooks              <- Jupyter notebooks. Naming convention is a number (for ordering),
│                             the creator's initials, and a short `-` delimited description,
│                             e.g. `1.0-jqp-initial-data-exploration.ipynb`.
│
├── scripts                <- Shell scripts
│
├── rl4co                        <- Source code # NOTE: WIP
│   ├── envs                     <- RL environments
│   ├── models                   <- Model scripts
│   ├── rl                       <- RL algorithms
│   ├── utils                    <- Utility scripts
│   │
│   ├── eval.py                  <- Run evaluation
│   └── train.py                 <- Run training
│
├── tests                  <- Tests of any kind
│
├── .env.example              <- Example of file for storing private environment variables
├── .gitignore                <- List of files ignored by git
├── .pre-commit-config.yaml   <- Configuration of pre-commit hooks for code formatting
├── .project-root             <- File for inferring the position of project root directory
├── Makefile                  <- Makefile with commands like `make train` or `make test`
├── pyproject.toml            <- Configuration options for testing and linting
├── requirements.txt          <- File for installing python dependencies
├── setup.py                  <- File for installing project as a package
└── README.md
