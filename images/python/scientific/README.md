# Scientific Computing Environment Docker Image

This Dockerfile sets up a Docker image with a basic scientific computing environment. It includes the installation of essential scientific packages such as NumPy, SciPy, Matplotlib, and Pandas. These packages are widely used for numerical computations, data analysis, and visualization in Python.

The image is based on the official Python image, ensuring compatibility and ease of use. Additional packages can be installed as needed by modifying this Dockerfile.

## Usage

1. **Build the Docker image:**
    ```sh
    docker build -t scientific-computing .
    ```

2. **Run a container from the image:**
    ```sh
    docker run -it --rm scientific-computing
    ```

## Installed Packages

- Python
- NumPy
- SciPy
- Matplotlib
- Pandas