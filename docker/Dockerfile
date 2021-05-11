# syntax=docker/dockerfile:experimental

FROM nvcr.io/nvidia/deepstream-l4t:5.0.1-20.09-samples as build

WORKDIR / 

RUN --mount=type=cache,id=apt-build,target=/var/cache/apt \
    apt update && apt install -y \
        git \
        wget \
        cmake \
        g++ && \
    rm -rf /var/lib/apt/lists/*

RUN git clone --depth=1 --single-branch --branch patch-1 https://github.com/mmeendez8/amirstan_plugin.git && \ 
    cd /amirstan_plugin && \ 
    git submodule update --init --progress --depth=1 && \
    mkdir build && \
    cd build && \
    cmake .. -DWITH_DEEPSTREAM=true -DTENSORRT_DIR=/usr/include/aarch64-linux-gnu && \
    make -j10
