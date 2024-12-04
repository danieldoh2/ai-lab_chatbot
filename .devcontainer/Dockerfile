# Use a base image
FROM debian:bullseye

# Install dependencies and Podman
RUN apt-get update && \
    apt-get install -y curl gnupg2 software-properties-common && \
    curl -fsSL https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/Debian_11/Release.key | gpg --dearmor -o /etc/apt/trusted.gpg.d/devel_kubic_libcontainers_stable.gpg && \
    echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/Debian_11/ /" > /etc/apt/sources.list.d/devel:kubic-libcontainers.list && \
    apt-get update && \
    apt-get install -y podman fuse-overlayfs slirp4netns && \
    apt-get clean

# Configure Podman for rootless usage
RUN mkdir -p /etc/containers && \
    echo "[registries.search]" >> /etc/containers/registries.conf && \
    echo "registries = ['docker.io']" >> /etc/containers/registries.conf

# Set environment variables
ENV XDG_RUNTIME_DIR=/tmp/run
ENV PODMAN_USERNS=keep-id

WORKDIR /workspace
