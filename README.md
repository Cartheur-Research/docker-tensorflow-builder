# docker-tensorflow-builder

Compile TensorFlow docker images instead of installing natively on your computer.

## Requirements

- `docker`
- `docker-compose`

## Usage

- Clone this repository:

```bash
git clone https://github.com/cartheur-research/docker-tensorflow-builder.git
```

### TensoFlow CPU

- Edit the `build.sh` file to modify TensorFlow compilation parameters. Then launch the build:

```bash
LINUX_DISTRO="debian-bookworm"
cd "tensorflow/$LINUX_DISTRO"

# Set env variables
export PYTHON_VERSION=3.10
export TF_VERSION_GIT_TAG=v2.16.1
export BAZEL_VERSION=7.1.1
export USE_GPU=0

# Build the Docker image
docker-compose build

# Start the compilation
docker-compose run tf

# You can also do:
# docker-compose run tf bash
# bash build.sh
```

### TensorFlow GPU

- Edit the `build.sh` file to modify TensorFlow compilation parameters. Then launch the build:

```bash
LINUX_DISTRO="debian-bookworm"
cd "tensorflow/$LINUX_DISTRO"

# Set env variables
export PYTHON_VERSION=3.10
export TF_VERSION_GIT_TAG=v2.16.1
export BAZEL_VERSION=7.1.1
export USE_GPU=1
export CUDA_VERSION=12.0
export CUDNN_VERSION=9.1
export NCCL_VERSION=2.4

# Build the Docker image
docker-compose build

# Start the compilation
docker-compose run tf

# You can also do:
# docker-compose run tf bash
# bash build.sh
```

---

- Refer to [tested build configurations](https://www.tensorflow.org/install/source#tested_build_configurations) to know which `BAZEL_VERSION` you need.
- Be patient, the compilation can be long.
- Enjoy your Python wheels in the `wheels/` folder.
- *Don't forget to remove the container to free the space after the build: `docker-compose rm --force`.*
