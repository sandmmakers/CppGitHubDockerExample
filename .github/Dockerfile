FROM ubuntu:24.04

# Prevent installing suggested and recommended packages
RUN echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/00-docker
RUN echo 'APT::Install-Recommends "0";' >> /etc/apt/apt.conf.d/00-docker

# Update the package repository
RUN apt-get update

# Install system packages
RUN apt-get install -y build-essential cmake ninja-build

# Create a non-root user
RUN useradd -ms /bin/bash user
USER user