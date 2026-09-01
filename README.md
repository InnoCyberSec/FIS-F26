# Fundamentals of InfoSec - Fall 2026

## Content

- Lab 1: Cryptography and Steganography
- Lab 2: Authentication

## Getting Started

The lab environment can be deployed as a VM or a network of docker containers.

> A VM is recommended for a more realistic experience with `systemd` and full docker engine installed. The container provides a more lightweight experience but some commands may not work as expected.

## Quick Start (VM)

1. Install the prerequisites for your platform.

    <details><summary>Windows</summary>

    1. Install Git, QEMU and Lima

        ```bash
        winget install -e --id Git.Git
        winget install -e --id SoftwareFreedomConservancy.QEMU
        winget install -e --id Lima.Lima
        ```

    1. Ensure "Windows Hypervisor Platform" is enabled in Windows Features.

        ![hv](https://i.imgur.com/VgFx651.png)

    1. Use `limactl` **only from Git Bash** (SSH connection may fail from Powershell).

    </details>

    <details><summary>Linux</summary>

    - Follow [this](https://christitus.com/vm-setup-in-linux/) guide to install QEMU/KVM for your distro. It mostly boils down to installing the following packages,

        ```bash
        qemu-kvm qemu-system qemu-utils
        ```

    - Install Lima

        ```bash
        VERSION=$(curl -fsSL https://api.github.com/repos/lima-vm/lima/releases/latest | jq -r .tag_name)
        curl -fsSL "https://github.com/lima-vm/lima/releases/download/${VERSION}/lima-${VERSION:1}-$(uname -s)-$(uname -m).tar.gz" | tar Cxzvm /usr/local
        ```

    </details>

    <details><summary>MacOS</summary>

    - Install Git, QEMU and Lima

        ```bash
        brew install git qemu lima
        ```

    </details>

1. Use the provided [`labenv.yaml`](./labenv.yaml) (adjust parameters as needed)

    ```bash
    # Start the VM from YAML template
    limactl start ./labenv.yaml # Press enter to proceed

    # Watch boot logs in another terminal
    tail -f ~/.lima/labenv/serial*.log
    ```

1. Troubleshooting (check `limactl -h`)

    ```bash
    limactl list           # List VMs
    limactl shell labenv   # SSH into the VM
    limactl restart labenv # Restart the VM
    limactl stop labenv    # Stop the VM
    limactl delete labenv  # Delete the VM
    limactl prune          # Prune garbage objects
    limactl start-at-login --enabled false # Disable VM autostart
    ```

1. Access at <http://localhost:3000>. It's recommended to go through the [default workshop](https://github.com/Sh3b0/interactive-labs/tree/main/workshop) first to get familiar with the environment, then launch a lab from this repo by URL (e.g., `https://github.com/InnoCyberSec/FIS-F26/tree/main/lab1`)

## Quick Start (Docker)

1. Ensure you have docker and docker compose plugin installed

    ```bash
    docker -v
    docker compose version
    ```

1. Run the environment

    ```bash
    docker compose up -d
    ```

1. Access at <http://localhost:3000>
