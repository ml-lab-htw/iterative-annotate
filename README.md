# Feedback-driven object detection
## Iterative model improvement for accuate annotations

This is a mono-repository that combines [NextJS Frontend](https://github.com/ml-lab-htw/iterative-annotate-frontend) and [Python FastAPI Backend](https://github.com/ml-lab-htw/iterative-annotate-backend).
The repositories are included as git submodules. Make sure to follow the instrcutions for a correct installation.
We are using docker compose to start all required services at once.

## Install Instructions

### 1. After you clone the project, pull all sub-repositories
> ```bash
>   git submodule update --init
> ```
    
### 2. Start docker compose
> ```bash
>   docker-compose up -d --build
> ```
    
### 3. Access Website
> [Open local web-UI](http://localhost:3000/)

---

## GPU-Support

> ⚠️ **Warning:** \
> \
> Please adapt the [docker-compose.yml](docker-compose.yml) and the [backend Dockerfile](backend/Dockerfile) to enable CUDA-Support on your Docker-Container.
Otherwise the backend may only run on the CPU.
>
> Example: docker-compose.yml
> ```yml
> services:
>   ...
> 
>   backend:
>     ...
>     environment:
>       ...
>       - NVIDIA_VISIBLE_DEVICES=all
>       - NVIDIA_DRIVER_CAPABILITIES=compute,utility
>     deploy:
>       resources:
>         reservations:
>           devices:
>             - driver: nvidia
>               count: all
>               capabilities: [gpu]
>    runtime: nvidia
>    ...
> ```
> 
> 
> Example: backend/Dockerfile
> ```Dockerfile
> # Use NVIDIA's CUDA base image
> FROM nvidia/cuda:11.8.0-cudnn8-runtime-ubuntu22.04
> 
> # Set environment variables for CUDA
> ENV NVIDIA_VISIBLE_DEVICES all
> ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
>
> ... (add torch/cuda to requirements.txt if )
> ... (Rest of the Dockerfile)
> ```
> 
> 
> Another option is to directly run the FastAPI Server on a GPU-capable device - [Instructions](https://github.com/ml-lab-htw/iterative-annotate-backend/blob/main/README.md)
> and connect the frontend manually to the exposed IP
