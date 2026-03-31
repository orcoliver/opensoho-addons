ARG BUILD_FROM=ghcr.io/hassio-addons/base:17.2.1
# Stage 1: Build OpenSoho
FROM golang:1.26-alpine AS builder
# Set the working directory inside the container
WORKDIR /app

# Install git and ca-certificates (needed for Go modules)
RUN apk add --no-cache git ca-certificates

# Clone the source code
ARG CACHE_BUST=5
RUN git clone https://github.com/orcoliver/opensoho.git .

# Download dependencies
RUN go mod download

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o opensoho .

# Stage 2: Final Image
FROM $BUILD_FROM

# Install necessary dependencies
RUN apk add --no-cache \
    openssh-client \
    ca-certificates

# Copy the binary from the builder stage
COPY --from=builder /app/opensoho /usr/bin/opensoho

# Copy rootfs
COPY rootfs /

# Set workdir
WORKDIR /data

# Metadata
ARG BUILD_ARCH
LABEL \
    io.hass.name="OpenSoho" \
    io.hass.description="OpenWrt Router Management for Home Assistant" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version="1.0.8" \
    maintainer="Jules"
