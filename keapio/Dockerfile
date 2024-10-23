# Use an official lightweight Alpine image as the base
FROM alpine:3.18

# Set environment variables
ENV KUBECTL_VERSION=v1.31.1 \
    CLUSTERCTL_VERSION=v1.8.4 \
    VCLUSTER_VERSION=v0.20.1

# Install curl, bash, and other utilities
RUN apk add --no-cache coreutils curl bash

# Install kubectl
RUN curl -LO "https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Install clusterctl
RUN curl -L "https://github.com/kubernetes-sigs/cluster-api/releases/download/${CLUSTERCTL_VERSION}/clusterctl-linux-amd64" -o clusterctl && \
    install -o root -g root -m 0755 clusterctl /usr/local/bin/clusterctl && \
    rm clusterctl

# Install vcluster
RUN curl -L "https://github.com/loft-sh/vcluster/releases/download/${VCLUSTER_VERSION}/vcluster-linux-amd64" -o vcluster && \
    install -o root -g root -m 0755 vcluster /usr/local/bin/vcluster && \
    rm vcluster

# Verify installations
RUN kubectl version --client && clusterctl version && vcluster --version

# Set entrypoint to bash so that users can interactively run commands
ENTRYPOINT ["/bin/bash"]
