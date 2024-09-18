# Start with a base image that has Go installed
FROM golang:1.23 AS builder

# Set environment variables
ENV GOBIN=/usr/local/bin

# Set environment variables
ENV OPERATOR_SDK_VERSION=v1.36.1

# Create a working directory
WORKDIR /workspace

# Clone the Operator SDK repository
RUN git clone https://github.com/operator-framework/operator-sdk.git

# Change directory to the cloned repository
WORKDIR /workspace/operator-sdk

# Checkout the specific version of Operator SDK
RUN git checkout ${OPERATOR_SDK_VERSION}

# Build the Operator SDK binary
RUN make install

# Use a minimal base image for the final image
FROM alpine:3.20

RUN apk add --no-cache make

# Create a working directory
WORKDIR /workspace

# Copy the built binary from the builder stage
COPY --from=builder /usr/local/bin/operator-sdk /usr/local/bin/operator-sdk

# Set the entrypoint for the container
ENTRYPOINT ["sh"]

