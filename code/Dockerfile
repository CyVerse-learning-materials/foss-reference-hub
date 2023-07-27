FROM jupyter/datascience-notebook:lab-4.0.1

WORKDIR /home/jovyan

COPY src/ /home/jovyan/src
COPY test_data/ /home/jovyan/test_data
COPY environment.yml example.ipynb /home/jovyan

RUN mamba env create -f /home/jovyan/environment.yml && \
    mamba clean --all --yes

