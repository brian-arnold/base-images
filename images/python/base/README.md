# Python base image

## Overview
This minimal Python base image is built on top of an Ubuntu base image. It includes a specified version of Python and is designed to be a lightweight starting point for Python applications.

## Features
- **Ubuntu Base**: Leverages the stability and security of the Ubuntu operating system.
- **Minimal Packages**: Only essential packages are included to keep the image size small and reduce attack surface.
- **Python Version**: Comes with a specified version of Python pre-installed.

## Usage
To use this image, you can pull it from the container registry and use it as a base image in your Dockerfile:

```dockerfile
FROM enigma/python-minimal:<tag>
```

Replace `<tag>` with the desired version tag of the image.

## Example
Here is an example of a Dockerfile using this minimal Python base image:

```dockerfile
FROM enigma/python-minimal:3.9

# Install additional dependencies if needed
RUN apt-get update && apt-get install -y \
    some-package \
    && rm -rf /var/lib/apt/lists/*

# Copy application code
COPY . /app

# Set working directory
WORKDIR /app

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Command to run the application
CMD ["python", "app.py"]
```

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
# Minimal Python base image
Base image with specified Python version, but with minimal additional packages installed.