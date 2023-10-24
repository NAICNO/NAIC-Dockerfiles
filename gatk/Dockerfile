FROM continuumio/miniconda3:23.9.0

# Working directory
WORKDIR /app
COPY environment.yml .

# Install Conda packages listed in the environment.yml
RUN conda update -n base -c defaults conda && \
    conda env create -f environment.yml

# Activate the environment
SHELL ["conda", "run", "-n", "myenv", "/bin/bash", "-c"]

# Set environment variables
ENV PATH /opt/conda/envs/myenv/bin:$PATH

# Install linux commands
RUN apt-get update && apt-get install -y procps
