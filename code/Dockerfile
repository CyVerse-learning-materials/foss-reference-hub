FROM jupyter/datascience-notebook:lab-4.0.1

USER root

# Install a few dependencies, text editing, and monitoring instances
RUN apt update && \
    apt install -y lsb-release apt-transport-https curl libfreetype6-dev pkg-config libx11-dev gcc less software-properties-common apt-utils glances htop nano 

# Install and configure jupyter lab
COPY jupyter_notebook_config.json /opt/conda/etc/jupyter/jupyter_notebook_config.json

# Add sudo to jovyan user
RUN apt update && \
    apt install -y sudo && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

ARG LOCAL_USER=jovyan
ARG PRIV_CMDS='/bin/ch*,/bin/cat,/bin/gunzip,/bin/tar,/bin/mkdir,/bin/ps,/bin/mv,/bin/cp,/usr/bin/apt*,/usr/bin/pip*,/bin/yum,/bin/snap,/bin/curl,/bin/tee,/opt'

RUN usermod -aG sudo jovyan && \
    echo "$LOCAL_USER ALL=NOPASSWD: $PRIV_CMDS" >> /etc/sudoers
RUN addgroup jovyan
RUN usermod -aG jovyan jovyan

RUN sudo apt-get update && apt-get install -y software-properties-common

# Update and clean package manager
RUN apt-get update --yes && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER jovyan
WORKDIR /home/jovyan

COPY src/ /home/jovyan/src
COPY test_data/ /home/jovyan/test_data
COPY environment.yml example.ipynb /home/jovyan

RUN mamba env create -f /home/jovyan/environment.yml && \
    mamba clean --all --yes

RUN echo "source conda activate dplpy" >> ~/.bashrc

EXPOSE 8888