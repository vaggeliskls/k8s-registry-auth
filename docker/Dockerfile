# syntax=docker/dockerfile:1

FROM alpine:3.20

# Update the package index
# Upgrade a specific package, for example 'openssl' due to security
RUN apk update && apk upgrade openssl

# Install requirements
RUN apk add --no-cache \
    kubectl \
    aws-cli
