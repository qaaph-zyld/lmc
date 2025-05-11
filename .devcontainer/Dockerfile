# Base image
FROM ubuntu:latest

# Install jq and other common dev tools
RUN apt-get update && apt-get install -y \
    jq \
    curl \
    git \
    sudo \
    python3-pip \
    python3-venv \
    && rm -rf /var/lib/apt/lists/*

# Create a non-root user 'vscode' if it doesn't exist and add to sudoers
RUN if ! id vscode > /dev/null 2>&1; then \
        useradd -m -s /bin/bash vscode && \
        echo "vscode ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/vscode && \
        chmod 0440 /etc/sudoers.d/vscode; \
    fi

# Set the default user to 'vscode'
USER vscode
CMD ["sleep", "infinity"]
