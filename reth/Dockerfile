# Use rust image as the builder base
FROM rust:1.70.0-bullseye AS builder

# Set the build profile to be maxperf by default
ENV BUILD_PROFILE=maxperf
ENV RUST_BACKTRACE=1

# Update and install dependencies
RUN apt-get update && apt-get -y upgrade && apt-get install -y libclang-dev pkg-config

# Copy base folder into docker context
RUN git clone https://github.com/paradigmxyz/reth --branch main

# Build reth
RUN cd reth && RUSTFLAGS="-C target-cpu=native" cargo build --profile $BUILD_PROFILE --features jemalloc

WORKDIR /reth/target/$BUILD_PROFILE

CMD ["reth node"]
