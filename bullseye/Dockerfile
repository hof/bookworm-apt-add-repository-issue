FROM debian:bullseye

RUN apt-get update && apt-get install -y lsb-release wget software-properties-common gnupg
RUN bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"
