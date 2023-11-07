# Benchmarking

This repository contains the Snakemake workflow to reproduce the benchmarking study for the global haplotype reconstruction methods presented in https://doi.org/10.1101/2023.10.16.562462.

The notebooks in the directory `workflow/notebooks/` can be used to reproduce the figures of Figure 4.

Here is a step-by-step guide on how to run this workflow.
1. Clone the repository of V-pipe 3.0 into your working directory: `git clone https://github.com/cbg-ethz/V-pipe.git`  
2. Go into the directory of the benchmarking study for the global haplotype reconstruction `cd V-pipe/resources/auxiliary_workflows/benchmark/resources/multi_setup`  
3. The parameters to reproduce the synthetic dataset of varying coverage is here: `config_varycoverage/params.csv` with the configuration file `config_varycoverage/config.yaml` where simulation mode, replicate number and methods to be executed are defined.  
4. The parameters to reproduce the synthetic dataset of varying distance pattern is here: `config_varyparams/params.csv` with the configuration file `config_varyparams/config.yaml` where simulation mode, replicate number and methods to be executed are defined.  
5. The parameters to reproduce the real dataset is here: `config_realdata/params.csv` with the configuration file `config_realdata/config.yaml` where replicate number and methods to be executed are defined.  
6. The methods to execute must be define in a Python script in this directory: `V-pipe/resources/auxiliary_workflows/benchmark/resources/method_definitions`
   - Haploclique: `V-pipe/resources/auxiliary_workflows/benchmark/resources/method_definitions/haploclique.py`  
   - PredictHaplo: `V-pipe/resources/auxiliary_workflows/benchmark/resources/method_definitions/predicthaplo.py`  
   - HaploConduct: `V-pipe/resources/auxiliary_workflows/benchmark/resources/method_definitions/haploconduct.py`  
   - CliqueSNV: `V-pipe/resources/auxiliary_workflows/benchmark/resources/method_definitions/cliquesnv.py`
7. Now the workflow is ready, go back to the directory `V-pipe/resources/auxiliary_workflows/benchmark/resources/multi_setup`.   
8. To install the needed Conda environments execute: `snakemake --conda-create-envs-only --use-conda -c1`.   
9. To submit the workflow to a lsf-cluster execute `./run_workflow.sh`, otherwise execute the workflow with `snakemake --use-conda -c1`
10. The workflow will provide the results in the directory `results`.
11. When the workflow has terminated and all result files were generated, figures from Figure 4 from the manuscript can be generated by executing the notebooks in  `workflow/notebooks/`.  