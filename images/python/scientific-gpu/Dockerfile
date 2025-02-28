# GPU-enabled scientific Python image
ARG OWNER=enigma-brain
ARG PYTHON_VERSION=3
#FROM nvidia/cuda:12.8.0-cudnn-devel-ubuntu24.04
FROM nvidia/cuda:12.2.0-devel-ubuntu22.04

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    DEBIAN_FRONTEND=noninteractive


# redefine the ARGs
ARG PYTHON_VERSION


# Install Python and system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    python${PYTHON_VERSION} \
    python${PYTHON_VERSION}-dev \
    python${PYTHON_VERSION}-venv \
    python3-pip \
    build-essential \
    libopenblas-dev \
    liblapack-dev \
    libhdf5-dev \
    libatlas-base-dev \
    gfortran \
    wget \
    git \
    curl \
    graphviz \
    && rm -rf /var/lib/apt/lists/*



# Create and activate virtual environment
# This avoids the externally-managed-environment error
RUN python${PYTHON_VERSION} -m venv --system-site-packages /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Upgrade pip and setuptools - necessary to avoid some erros in package installations
RUN pip install --no-cache-dir --upgrade pip setuptools wheel

# Install common scientific packages
COPY ./images/python/scientific/requirements-common.txt .
RUN pip install --no-cache-dir -r requirements-common.txt

# Install GPU-specific packages
COPY ./images/python/scientific-gpu/requirements-gpu.txt .
RUN pip install --no-cache-dir -r requirements-gpu.txt


# Default command
CMD ["python", "-c", "import torch; print(f'GPU available: {torch.cuda.is_available()}')"]