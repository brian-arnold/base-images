# GPU-enabled scientific Python image
ARG OWNER=enigma-brain
ARG PYTHON_VERSION=3.9
FROM nvidia/cuda:12.2.0-devel-ubuntu20.04


# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    DEBIAN_FRONTEND=noninteractive

# redefine the ARGs
ARG PYTHON_VERSION
# Create a non-root user
RUN groupadd -r jovyan && useradd -r -g jovyan jovyan

# Set working directory
WORKDIR /src

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
    && rm -rf /var/lib/apt/lists/*

# Create and activate virtual environment
# This avoids the externally-managed-environment error
RUN python${PYTHON_VERSION} -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Install common scientific packages
COPY ./images/python/scientific/requirements-common.txt .
RUN pip install --no-cache-dir -r requirements-common.txt

# Install GPU-specific packages
COPY ./images/python/scientific-gpu/requirements-gpu.txt .
RUN pip install --no-cache-dir -r requirements-gpu.txt


# Default command
CMD ["python", "-c", "import torch; print(f'GPU available: {torch.cuda.is_available()}')"]