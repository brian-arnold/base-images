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


# Define build arguments
ARG USER_UID=1000
ARG USER_GID=1000
ARG USER_NAME=jovyan


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

# Setup user and group with given UID and GID as well as given name
# If it already exists, change the group name or user name to the given name
RUN if ! getent group ${USER_GID} > /dev/null; then \
    groupadd -g ${USER_GID} ${USER_NAME}; \
    else \
    CURRENT_GROUP=$(getent group ${USER_GID} | cut -d: -f1) && \
    groupmod -n ${USER_NAME} ${CURRENT_GROUP}; \
    fi && \
    if ! getent passwd ${USER_UID} > /dev/null; then \
    useradd -m -u ${USER_UID} -g ${USER_GID} ${USER_NAME}; \
    else \
    CURRENT_USER=$(getent passwd ${USER_UID} | cut -d: -f1) && \
    usermod -l ${USER_NAME} ${CURRENT_USER}; \
    fi && \
    chown -R ${USER_NAME}:${USER_GID} /opt/venv
# Switch to the new user
USER ${USER_NAME}
WORKDIR /home/${USER_NAME}

# Install common development tools in the virtual environment
RUN pip install --upgrade pip setuptools wheel

# Install from requirements file
COPY ./images/python/base/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt


# TODO: Add restrcited user for running the container
# RUN groupadd -r jovyan && useradd -r -g jovyan jovyan

# Default command
CMD ["bash"]