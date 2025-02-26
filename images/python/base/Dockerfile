ARG GIT_SHA=latest
ARG OWNER=enigma-brain
ARG PLATFORM=linux/amd64
FROM --platform=${PLATFORM} ubuntu:24.04

ARG PYTHON_VERSION=3.12
ARG GIT_SHA
LABEL org.opencontainers.image.revision=${GIT_SHA}

# Avoid prompts from apt
ENV DEBIAN_FRONTEND=noninteractive \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on


# Install system dependencies and Python
# TODO: consider revisiting this list and prune
RUN apt-get update && apt-get install -y --no-install-recommends \
    python${PYTHON_VERSION} \
    python${PYTHON_VERSION}-venv \
    python${PYTHON_VERSION}-dev \
    build-essential \
    curl \
    git \
    vim \
    wget \
    unzip \
    ffmpeg \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Create and activate virtual environment
# This avoids the externally-managed-environment error
RUN python${PYTHON_VERSION} -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Install common development tools in the virtual environment
RUN pip install --upgrade pip setuptools wheel

# TODO: Add restrcited user for running the container
# RUN groupadd -r jovyan && useradd -r -g jovyan jovyan

# Default command
CMD ["bash"]