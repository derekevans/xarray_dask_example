FROM ubuntu:22.04

RUN apt-get update

# Necessary for installing tzdata non-interactively
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Etc/UTC

# Install tools 
RUN apt-get install software-properties-common tzdata -y

# Install python3.11
RUN add-apt-repository ppa:deadsnakes/ppa -y && \
    apt-get update -y && \
    apt-get install python3.11 python3.11-venv python3.11-dev python3.11-distutils libffi-dev -y

# Create ubuntu user, switch to this user, and cd to user home directory
RUN useradd --create-home --shell /bin/bash ubuntu
USER ubuntu
ENV HOME=/home/ubuntu
WORKDIR $HOME

# Install venv
RUN python3.11 -m venv ~/python/envs/venv

# Enable venv
ENV PATH="/home/ubuntu/python/envs/venv/bin:$PATH"

# Install other Python dependencies
COPY requirements.txt /home/ubuntu/python/envs/venv/requirements.txt
RUN pip install -r /home/ubuntu/python/envs/venv/requirements.txt

# Create directory to mount data volume to
RUN mkdir data

# Run the worker  
# TODO: update this to take nthreads and memory limit from user input 
CMD dask worker tcp://scheduler:8786 --nworkers 1 --nthreads 3 --memory-limit 4G