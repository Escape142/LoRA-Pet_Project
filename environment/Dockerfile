# Stage 1
# Use base conda image to reduce time
FROM continuumio/miniconda3:latest AS compile-image
# Specify py version
ENV PYTHON_VERSION=3.8

# Install apt libs
RUN apt-get update && \
    apt-get install -y curl git wget software-properties-common git-lfs tmux && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists*


# Create our conda env
COPY environment.yml /tmp/environment.yml
RUN conda env create -f /tmp/environment.yml

# Clean up
RUN conda clean -a -y
RUN rm /tmp/environment.yml

# Below is copied from https://github.com/huggingface/accelerate/blob/main/docker/accelerate-gpu/Dockerfile
# We don't install pytorch here yet since CUDA isn't available
# instead we use the direct torch wheel
ENV PATH /opt/conda/envs/peft/bin:$PATH
# Activate our bash shell
RUN chsh -s /bin/bash
SHELL ["/bin/bash", "-c"]

# Stage 2
FROM nvidia/cuda:12.2.2-devel-ubuntu22.04 AS build-image
COPY --from=compile-image /opt/conda /opt/conda
ENV PATH /opt/conda/bin:$PATH

RUN chsh -s /bin/bash
SHELL ["/bin/bash", "-c"]

# Install apt libs necessary including git
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl git wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install necessary packages using pip
RUN source activate peft && \ 
    python3 -m pip install --no-cache-dir bitsandbytes optimum auto-gptq && \
    python3 -m pip install --no-cache-dir https://github.com/casper-hansen/AutoAWQ/releases/download/v0.2.4/autoawq-0.2.4-cp38-cp38-linux_x86_64.whl && \
    python3 -m pip install --no-cache-dir https://github.com/casper-hansen/AutoAWQ_kernels/releases/download/v0.0.6/autoawq_kernels-0.0.6-cp38-cp38-linux_x86_64.whl && \
    python3 -m pip install -U --no-cache-dir librosa "soundfile>=0.12.1" scipy git+https://github.com/huggingface/transformers git+https://github.com/huggingface/accelerate peft[test]@git+https://github.com/huggingface/peft && \
    pip install aqlm[gpu]>=1.0.2 hqq && \
    pip freeze | grep transformers

# Activate the conda env by default
RUN echo "source activate peft" >> ~/.profile

# Activate the virtualenv
CMD ["/bin/bash"]