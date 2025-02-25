ARG GIT_SHA=latest
ARG OWNER=enigma-brain
# minimalistic Python image
FROM python:3.11-slim
LABEL org.opencontainers.image.revision=${GIT_SHA}

# Set environment variables
# PYTHONDONTWRITEBYTECODE: Prevents Python from writing pyc files to disc
# PYTHONUNBUFFERED: Prevents Python from buffering stdout and stderr
# PIP_NO_CACHE_DIR: Prevents pip from creating a cache directory
# DEBIAN_FRONTEND: Prevents debconf from prompting for input
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    DEBIAN_FRONTEND=noninteractive

# Set working directory
WORKDIR /src

# Install minimal system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    ca-certificates \
    git \
    && rm -rf /var/lib/apt/lists/*

# Copy and install base requirements
COPY ./images/python/minimal/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Default command
CMD ["python", "-c", "print('Python Minimal Base Image')"]
