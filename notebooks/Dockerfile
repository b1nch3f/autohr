# Use Ubuntu 20.04 as the base image
FROM ubuntu:22.04

# Set non-interactive mode
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install essential packages
# Add the deadsnakes PPA repository
RUN apt-get update -y \
    && apt-get install -y software-properties-common \
    && add-apt-repository ppa:deadsnakes/ppa -y \
    && apt-get update -y \
    && apt-get install -y --no-install-recommends \
        python3.10 \
        python3.10-dev \
        python3.10-distutils \
        python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Create symbolic links for Python and pip if they don't exist
RUN if [ ! -f /usr/bin/python ]; then ln -s /usr/bin/python3.10 /usr/bin/python; fi \
    && if [ ! -f /usr/bin/pip ]; then ln -s /usr/bin/pip3.10 /usr/bin/pip; fi

WORKDIR /home

COPY ./requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# Specify the command to run when the container starts
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--allow-root"]
