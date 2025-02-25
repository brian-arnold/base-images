# Accept Git SHA as a build argument
ARG OWNER=enigma-brain
ARG GIT_SHA=latest
FROM ghcr.io/${OWNER}/python-minimal:${GIT_SHA}
# Add Git SHA as a label for traceability
LABEL org.opencontainers.image.revision=${GIT_SHA}

# Install system dependencies for scientific packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libopenblas-dev \
    liblapack-dev \
    libhdf5-dev \
    libatlas-base-dev \
    gfortran \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Install common scientific Python packages
COPY ./images/python/scientific/requirements-common.txt .
RUN pip install --no-cache-dir -r requirements-common.txt

# Default command
CMD ["python", "-c", "import numpy; print('Scientific Common Base Image')"]
