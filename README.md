# Objective

The objective of this reposisitory is to demonstrate distributed computing using dask and xarray.  

## Docker Compose
Docker Compose is used to create containers running Jupyter Lab, Dask Scheduler, and Dask Worker.  The purpose of using Docker Compose rather than using a Dask LocalCluster was to better resemble distributed computing across multiple nodes.  For this example, the cluster contains three worker nodes.  Each node has one worker process, three threads, and a memory limit of 4GB.  Also, a /data volume is created and attached to each container.

## Install

To install the environment for this repo, you first need to have Docker Desktop installed.  Once installed:

```sh
git clone https://github.com/derekevans/xarray_dask_example
cd xarray_dask_example
make docker/start
```

### Jupyter Lab
Jupyter Lab is accessible at http://localhost:8890/lab.  The xarray_dask_example.ipynb notebook provides an example of using the cluster built with Docker Compose to perform distributed computing with xarray and Dask.

### Dask Dashboard
The Dask dashboard is accessible at http://localhost:8789/status and can be used to monitor computations.

## TODO
1. Change dask worker nworkers, nthreads, and memory-limit arguments in Dockerfile based on user input.  



