FROM debian:bookworm

RUN apt-get update && apt-get install -y lsb-release wget software-properties-common gnupg curl
RUN wget -qO- https://apt.llvm.org/llvm-snapshot.gpg.key | tee /etc/apt/trusted.gpg.d/apt.llvm.org.asc

# workaround #2: install another repository in /etc/apt/sources.list.d (in .list format)
RUN mkdir -p --mode=0755 /usr/share/keyrings
RUN curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.noarmor.gpg | tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
RUN curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.tailscale-keyring.list | tee /etc/apt/sources.list.d/tailscale.list

RUN apt-add-repository "deb http://apt.llvm.org/bookworm/ llvm-toolchain-bookworm-17 main"

RUN apt-get update && apt-get install -y clang-17