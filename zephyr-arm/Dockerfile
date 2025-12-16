FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

# Core dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    ccache \
    cmake \
    device-tree-compiler \
    dfu-util \
    file \
    gcc \
    gcc-multilib \
    g++-multilib \
    git \
    gperf \
    libsdl2-dev \
    libmagic1 \
    make \
    ninja-build \
    python3-dev \
    python3-venv \
    python3-tk \
    wget \
    xz-utils

# Install the Zephyr toolchain only for arm-zephyr-eabi
ARG ZEPHYR_SDK_VERSION=0.17.4
RUN wget -q https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v${ZEPHYR_SDK_VERSION}/zephyr-sdk-${ZEPHYR_SDK_VERSION}_linux-x86_64_minimal.tar.xz \
  && mkdir -p /opt/toolchains \
  && tar xf zephyr-sdk-${ZEPHYR_SDK_VERSION}_linux-x86_64_minimal.tar.xz -C /opt/toolchains \
  && /opt/toolchains/zephyr-sdk-${ZEPHYR_SDK_VERSION}/setup.sh -c -t arm-zephyr-eabi \
  && rm zephyr-sdk-${ZEPHYR_SDK_VERSION}_linux-x86_64_minimal.tar.xz

# Create python virtual environment
RUN python3 -m venv /.venv \
&& /.venv/bin/pip install --no-cache-dir \
west protobuf grpcio-tools

# Set environment variables
ENV CMAKE_PREFIX_PATH=/opt/toolchains
ENV VIRTUAL_ENV=/.venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"
