FROM buildpack-deps:stretch

# Install required libraries
RUN apt-get update -y --fix-missing
RUN apt-get install -y \
    build-essential \
    libgflags-dev \
    libsnappy-dev \
    zlib1g-dev \
    libbz2-dev \
    liblz4-dev

# Install and compile rocksdb
## Download last specific version (at time of writing) to make docker images build predictable
WORKDIR /tmp
RUN wget -O rocksdb.tar.gz https://github.com/facebook/rocksdb/archive/v6.0.2.tar.gz
RUN tar zxf rocksdb.tar.gz
WORKDIR /tmp/rocksdb-6.0.2
RUN DEBUG_LEVEL=0 make shared_lib
RUN DEBUG_LEVEL=0 make install-shared

WORKDIR /

# Remove unnecesary dependencies and files
RUN apt-get remove -y \
    build-essential \
    curl \
    && rm -rf /tmp/rocksdb-6.0.2
