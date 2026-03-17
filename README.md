# Blender Docker Headless

[![actions](https://github.com/gerasim13/blender-docker-headless/actions/workflows/docker-build-push.yml/badge.svg)](https://github.com/gerasim13/blender-docker-headless/actions/workflows/docker-build-push.yml)
[![docker](https://img.shields.io/docker/pulls/gerasim13/blender)](https://hub.docker.com/r/gerasim13/blender)
[![license](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

:rocket: This repository provides a bunch of Docker images for Blender optimized for **<ins>headless</ins>** rendering. It fully supports both **<ins>EEVEE</ins>** and **<ins>CYCLES</ins>** render engines with GPU acceleration through **EGL**.

Current default target:

- Blender `4.5.1 LTS`
- CUDA `12.8.1`
- Ubuntu `24.04`

## Usage

```bash
docker run -it --rm --gpus all -v $(pwd):/workspace -w /workspace gerasim13/blender:blender-4.5.1-cuda12.8.1-ubuntu24.04
```

## Build

```bash
docker build -t gerasim13/blender:blender-4.5.1-cuda12.8.1-ubuntu24.04 . --build-arg BLENDER_VERSION=4.5.1 --build-arg UBUNTU_CUDA_VERSION=12.8.1-cudnn-devel-ubuntu24.04
```

## Test

```bash
docker run --rm --gpus all -v $(pwd):/workspace -w /workspace gerasim13/blender:blender-4.5.1-cuda12.8.1-ubuntu24.04 blender -b --python tests/render_eevee.py
```

```bash
docker run --rm --gpus all -v $(pwd):/workspace -w /workspace gerasim13/blender:blender-4.5.1-cuda12.8.1-ubuntu24.04 blender -b --python tests/render_cycles.py
```

## Version Notes

- Blender `4.5 LTS` is the current long-term support line from Blender, supported until July 2027.
- Blender `4.5.1` is the first bugfix release in that LTS line.
- Cycles OptiX in Blender `4.5` requires an NVIDIA driver new enough for OptiX support. Blender's release notes list `535` as the minimum driver version for OptiX in this release line.

## Key

- [EGL support](https://archive.blender.org/developer/D6585) and [libglvnd](https://github.com/NVIDIA/libglvnd).
- Enable the `graphics` capability for environment variable `NVIDIA_DRIVER_CAPABILITIES`, [doc](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/docker-specialized.html#driver-capabilities).

## GitHub Actions

The GitHub Actions workflow in [.github/workflows/docker-build-push.yml](.github/workflows/docker-build-push.yml) builds and pushes the Docker image to Docker Hub for each Blender version and Ubuntu version.

## Resources

EGL rendering:

- https://c.pgdm.ch/notes/eevee-docker-gpu
- https://archive.blender.org/developer/D6585
- https://archive.blender.org/developer/D15555
- https://projects.blender.org/blender/blender/commit/3195a381200eb98e6add8b0504f701318186946d
- https://github.com/NVIDIA/libglvnd

Nvidia container toolkit:

- https://blenderartists.org/t/belender-4-2-1-eevee-does-not-work-inside-docker/1551491/6
- https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/docker-specialized.html
- https://download.nvidia.com/XFree86/Linux-x86_64/460.56/README/installedcomponents.html

Blender images:

- https://github.com/ranchcomputing/blender-cpu-image
- https://github.com/nytimes/rd-blender-docker/tree/master
