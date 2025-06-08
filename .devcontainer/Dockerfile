FROM pytorch/pytorch:2.7.0-cuda12.8-cudnn9-runtime

# Install common tools
RUN apt-get update && apt-get install -y \
    git curl nano python3-venv && \
    rm -rf /var/lib/apt/lists/*

# Create a non-root user and set permissions
ARG USERNAME=devuser
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && mkdir -p /workspace \
    && chown -R $USERNAME:$USERNAME /workspace

# Install JupyterLab in the base conda environment as root
USER root
RUN /opt/conda/bin/conda install -y jupyterlab && conda clean -afy
# Ensure devuser owns all files in /workspace
RUN chown -R devuser:devuser /workspace
USER $USERNAME

USER $USERNAME
WORKDIR /workspace

# Make conda available for devuser
ENV PATH="/opt/conda/bin:$PATH"

# Expose Jupyter
EXPOSE 8888

ENV PATH="/workspace/venv/bin:$PATH"