FROM resinplayground/jetson-nano-cuda-cudnn-opencv:v0.2-slim

ENV DEBIAN_FRONTEND noninteractive

# Update NVIDIA Signing key
# See also https://forums.developer.nvidia.com/t/gpg-error-http-developer-download-nvidia-com-compute-cuda-repos-ubuntu1804-x86-64/212904/3
RUN apt-key del 7fa2af80 && \
    apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/3bf863cc.pub

# Install commonly used dependencies
RUN apt-get update && \
    apt-get install -y jq wget
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    apt-get install -y nodejs

# Start Darknet Install
RUN git clone --depth 1 -b odc https://github.com/opendatacam/darknet /var/local/darknet

WORKDIR /var/local/darknet

# COPY Makefile
COPY docker/build/xavier/Makefile Makefile

RUN make
