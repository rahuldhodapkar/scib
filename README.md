# Benchmarking atlas-level data integration in single-cell genomics

This repository contains code and analysis for the benchmarking study for data integration tools.
In this study, we benchmark 10 methods ([see here](##tools)) with 4 combinations of preprocessing steps leading to 40 methods combinations on
60 batches of gene expression and chromatin accessibility data.

We created the python module `scIB` to streamline the integration process and to integrate it into
a scanpy workflow. Furthermore, we created an environment to allow easy integration of R integration methods
into the scanpy workflow.

The scib python module is in the folder scIB. It can be installed using `pip install -e .` run in the root directory.
R helper functions for R integration methods can be found in the `R` directory.
The `scripts` folder contains scripts for preparing the data, running the methods, postprocessing and calculation of the metrics.
The `notebooks` folder contains jupyter notebooks for testing and demonstrating functions of the `scIB` package as well as notebooks
for preprocessing of the data.



## Installation
To reproduce the results from this study, three different conda environments are needed.
There are different environments for the python integration methods, the R integration methods and
the conversion of R data types to anndata objects.

For the installation of conda, follow [these](https://conda.io/projects/conda/en/latest/user-guide/install/index.html) instructions
or use your system's package manager. The environments have only been tested on linux operating systems
although it should be possible to run the pipeline using Mac OS.

To create the conda environments use the `.yml` files in the `envs` directory.
To install the envs, use
```bash
conda env create -f FILENAME.yml
``` 
To set the correct paths so that R the correct R libraries can be found, copy `env_vars_activate.sh` to `etc/conda/activate.d/`
and `env_vars_deactivate.sh` to `etc/conda/deactivate.d/` to every environment.
In the `conosTest` environment, R packages need to be installed manually.
Activate the environment and install the packages `scran`, `Seurat` and `Conos` in R. `Conos` needs to be installed using R devtools.
See [here](https://github.com/hms-dbmi/conos).


## Running the integration methods
This package allows to run a multitude of single cell data integration methods in both `R` and `python`.
We use [Snakemake](https://snakemake.readthedocs.io/en/stable/) to run the pipeline.
The parameters of the run are configured using the `config.yaml` file.
See the `DATA_SCENARIOS` section to change the data used for integration.
The script expects one `.h5ad` file containing all batches per data scenario.

To load the config file run `snakemake --configfile config.yaml`.
Define the number of CPU threads you want to use with `snakemake --cores N_CORES`. To produce an overview of tasks that will be run, use `snakemake -n`.
To run the pipeline, simply run `snakemake`.

## Tools
Tools to be compared include:
- [Seurat v3](https://github.com/satijalab/seurat)
- [TrVae](https://github.com/theislab/trvae)
- [scVI](https://github.com/YosefLab/scVI)
<!--- - [scANVI](https://github.com/chenlingantelope/HarmonizationSCANVI) -->
- [CONOS](https://github.com/hms-dbmi/conos) [tutorial](https://htmlpreview.github.io/?https://github.com/satijalab/seurat.wrappers/blob/master/docs/conos.html)
- [MNN](https://github.com/chriscainx/mnnpy)
- [Scanorama](https://github.com/brianhie/scanorama)
- RISC
- [LIGER](https://github.com/MacoskoLab/liger)
- [BBKNN](https://github.com/Teichlab/bbknn)
- [Harmony](https://github.com/immunogenomics/harmony)
<!--- - [scMerge](https://github.com/SydneyBioX/scMerge)
- [scAlign](https://github.com/quon-titative-biology/scAlign) -->
<!--- - BBKNN + [scAEspy](https://gitlab.com/cvejic-group/scaespy)? -->
