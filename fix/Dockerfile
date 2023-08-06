FROM debian:bookworm

RUN apt-get update && apt-get install -y wget software-properties-common

# use the fixed version
COPY ./apt-add-repository /usr/bin/apt-add-repository

RUN wget -qO- https://apt.llvm.org/llvm-snapshot.gpg.key | tee /etc/apt/trusted.gpg.d/apt.llvm.org.asc
RUN apt-add-repository "deb http://apt.llvm.org/bookworm/ llvm-toolchain-bookworm-17 main"
RUN apt-get update && apt-get install -y clang-17