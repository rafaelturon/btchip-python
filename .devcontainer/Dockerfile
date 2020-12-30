# download and use an existing image which already has Conda installed and set up
FROM debian:stretch-slim

# Configure apt
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get -y install --install-recommends python3-pip

# Install git, process tools, lsb-release (common in install instructions for CLIs)
RUN apt-get -y install git procps lsb-release 

# Install any missing dependencies for enhanced language service
RUN apt-get -y install libicu[0-9][0-9]

# Install device daemon
RUN apt-get -y install udev

# Install Development libraries
RUN apt-get -y install libudev-dev

# Install USB HID-class devices libraries
RUN apt-get -y install libusb-1.0-0-dev
RUN apt-get -y install libhidapi-libusb0

# Python Version
RUN alias python=python3

RUN mkdir /workspace
WORKDIR /workspace

# Install Python dependencies from requirements.txt and requirements_dev.txt
# COPY requirements/* /workspace/requirements/
# COPY requirements.txt* /workspace/
# RUN pip3 install hidapi
RUN pip3 install ecdsa

RUN wget -q -O - https://raw.githubusercontent.com/LedgerHQ/udev-rules/master/add_udev_rules.sh | bash
#RUN python3 setup.py instal

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog

# Set PACKAGE_VERSION to localdev
ENV PACKAGE_VERSION=localdev

# Set the default shell to bash rather than sh
ENV SHELL /bin/bash

# Set the PYTHONPATH for testing
ENV PYTHONPATH=/workspace/app

#RUN python3 setup.py install