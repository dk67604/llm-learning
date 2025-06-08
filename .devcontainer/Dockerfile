FROM pytorch/pytorch:2.7.0-cuda12.8-cudnn9-runtime

# Install common tools
RUN apt-get update && apt-get install -y \
    git curl nano && \
    rm -rf /var/lib/apt/lists/*

# Install JupyterLab
RUN pip install --upgrade pip && \
    pip install jupyterlab

# Expose Jupyter
EXPOSE 8888

WORKDIR /workspace
