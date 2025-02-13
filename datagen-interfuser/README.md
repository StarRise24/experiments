# Data generation

This folder contains tools for generating InterFuser datasets.

## Instructions

You can modify the files in `routegen/src` to customice the dataset generation:
- `routegen/src/generate_yamls.py`: You can modify fps, waypoints distribution strength, etc.
- `routegen/src/generate_route_configs.py` and `routegen/src/generate_route_configs.py`: If you don't need all weather, you can modify these scripts.

Then, generate route_configs and copy them to the idun folder:
    
```sh
cd routegen
make route_configs
make copy_idun
```

## To Idun and beyond

Then we'd like to generate the dataset on Idun.
In theory, the following should be enough:

```sh
cd idun
make job CARLA_IMAGE=mathiaswold/carla:0.9.14 INTERFUSER_COMMIT=0.9.14
```
and wait. This will:
- build CARLA and InterFuser docker images
- convert those to Singularity/Apptainer .sif-images
- rsync those to Idun
- submit a Slurm job to generate data

All files are stored under `~/work/thesis/datagen` on Idun,
however this can be changed by modifying `$IDUN_WORKDIR` in the `Makefile`.

## Data generation on local clients
You can also generate data on a local machine using Docker Compose. See the `./local/run.sh` script for details. You can specify the number of parallel executions. Example:

Generate and copy routes:
```sh
cd routegen
make route_configs
make copy_local
```
    
Start data generation:
```sh
cd local
NUM_JOBS=3 ./run.sh
```
