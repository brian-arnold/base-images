# base-images
A collection of Docker base images for use across Enigma projects

For example, to build the scientific-gpu image, execute the following command from this directory:
`docker build --no-cache -t at-docker.stanford.edu:5000/<insert_name_here>:latest -f ./images/python/scientific-gpu/Dockerfile .`