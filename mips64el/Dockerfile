FROM debian:9
COPY sources.list /etc/apt/sources.list
# Add the foreign architecture we want and install dependencies
RUN dpkg --add-architecture mips64el && \
    apt-get update

RUN DEBIAN_FRONTEND=noninteractive \
    apt-get install -y --no-install-recommends \
        eatmydata

RUN DEBIAN_FRONTEND=noninteractive eatmydata \
    apt-get install -y --no-install-recommends \
        gcc-mips64el-linux-gnuabi64

RUN DEBIAN_FRONTEND=noninteractive eatmydata \
    apt-get build-dep -yy -a mips64el qemu

# Specify the cross prefix for this image (see tests/docker/common.rc)
ENV QEMU_CONFIGURE_OPTS --cross-prefix=mips64el-linux-gnuabi64-

# Install extra libraries to increase code coverage
RUN DEBIAN_FRONTEND=noninteractive eatmydata \
    apt-get install -y --no-install-recommends \
        libbz2-dev:mips64el \
        liblzo2-dev:mips64el \
        librdmacm-dev:mips64el \
        libsnappy-dev:mips64el
