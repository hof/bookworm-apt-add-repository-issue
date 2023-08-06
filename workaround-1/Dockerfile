FROM debian:bookworm

RUN apt-get update && apt-get install -y lsb-release wget software-properties-common gnupg
RUN wget -qO- https://apt.llvm.org/llvm-snapshot.gpg.key | tee /etc/apt/trusted.gpg.d/apt.llvm.org.asc

# workaround #1: at least one line (comment or not) in /etc/sources.list
RUN echo "#" | tee /etc/apt/sources.list

RUN apt-add-repository "deb http://apt.llvm.org/bookworm/ llvm-toolchain-bookworm-17 main"

RUN apt-get update && apt-get install -y clang-17