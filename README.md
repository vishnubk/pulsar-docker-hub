# pulsar-docker-hub

---

# Pulsar Software Docker Files

This repository provides Dockerfiles for various pulsar software packages, including Peasoup, Dedisp, Presto, DSPSR, and PSRCHIVE. 

For GPU-Based software like Peasoup and Dedisp that run on GPUs, you may need to use different Dockerfiles depending on your environment and GPU capabilities.

## Available Dockerfiles

- **CUDA 12 Support**:  
  For Peasoup and Dedisp to run on CUDA 12, use `peasoup-sm89-dockerfile`.

- **CUDA Versions Prior to 12**:  
  If you're running a version of CUDA earlier than 12, use `peasoup-sm61-dockerfile`.

## Building Your Docker Image

To build a Docker image using a specific Dockerfile, run the following command, substituting in the appropriate Dockerfile and image name:

```bash
docker build -f $docker_filename -t $docker_image_name_you_like .
```

### Example for CUDA 12:

```bash
docker build -f peasoup-sm89-dockerfile -t peasoup:sm89 .
```




## GPU Compute Flags

Depending on the specific GPU in your system, you may need to set appropriate compute flags for `nvcc` during the build process. These flags ensure that the Docker container is optimized for your GPU architecture. You can look up the appropriate compute capability for your GPU on [NVIDIA's CUDA GPUs page](https://developer.nvidia.com/cuda-gpus).

Once you've identified the correct compute capability, you can pass it as a build argument to the `Makfile` inside [Dedisp](https://github.com/vishnubk/dedisp/tree/master) or [Peasoup](https://github.com/vishnubk/peasoup).

### Example:

If your GPU's compute capability is 8.9 (e.g., for an NVIDIA L40), add ```GPU_ARCH_FLAG = -arch=sm_89``` to your Makefile.inc file inside dedisp. You can see an example [here](https://github.com/vishnubk/dedisp/blob/sm_89/Makefile.inc)

