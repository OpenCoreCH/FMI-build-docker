# FMI Build Docker Image

Docker images that facilitate the compilation of the FMI library by installing/compiling the correct version of all dependencies. Images are based on Amazon's [aws-lambda-base-images](https://github.com/aws/aws-lambda-base-images).

## Usage

To compile the library for the `python36` runtime:
```sh
docker build -t python36build:1.0 -f Dockerfile.python3.6 .
docker run -it --mount type=bind,source=/path_to/FMI/,target=/opt/smi/ --rm python36build:1.0 bash -c "mkdir -p /opt/smi/python/build/ && cd /opt/smi/python/build/ && cmake -DPython3_INCLUDE_DIR=/usr/include/python3.6m/ .. && make"
```

The variable `Python3_INCLUDE_DIR` only needs to be set for the `python36` container, for all others `cmake ..` can be used.
