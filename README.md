# README: Quick-Dev-Vagrant

## Overview

Quick-Dev-Vagrant simplifies creating a DevOps environment with Vagrant, automating the setup of virtual machines (VMs) for development, testing, or production environments. It uses a configuration-driven approach with a `boxes.yml` file and includes a controller VM with Ansible, removing the need for local Ansible installations. Designed originally for personal use, it's now made available for anyone with similar needs. For more details on Vagrant, visit [Vagrant's official website](https://www.vagrantup.com/).

### Important Note

This project's first release has only been tested on Apple Silicon with Parallels Desktop 19 Pro. It's released under the "release early, release often" principle to gather feedback and improve continuously.

> "Release early, release often." - Eric S. Raymond

## Prerequisites

Before starting, ensure you have the following installed on your system:
- Vagrant
- VirtualBox or Parallels (depending on your VM provider preference)

Note: Ansible installation on your local machine is not required as the controller VM includes Ansible.

### Quickstart

1. Install [Vagrant](https://www.vagrantup.com/downloads) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (or Parallels).
2. Clone this repository and navigate into it.
3. Run `vagrant up` to provision and start your VMs using the default `boxes.yml` configuration.

## Tested Environment

- **OS:** macOS 14.3.1, Sonoma
- **Architecture:** ARM64, Apple Silicon M1
- **Vagrant Version:** 2.4.1
- **Parallels Version:** 19.3.0 Pro

## Limitations

This project is currently tested only with Debian-based Vagrant boxes. Compatibility with other Unix-like systems is potential but untested, and may require additional configuration steps.

## Installation

1. Clone this repository to your local machine.
2. Navigate to the cloned directory.
3. Check `boxes.yml` is configured as per your needs.

Use the following commands to set up a Python virtual environment and install dependencies inside the VM:

```bash
cd /vagrant
python3 -m venv venv 
source venv/bin/activate 
pip install -r requirements.txt
```

## Future Improvements / TODO

- Environment-specific Configuration Directories: 
  - Introduce a environments/ directory for tailored setups.
- Enhanced Environment Flexibility:
  - Consider replacing the controller VM with a container where beneficial and exploring mixed container-VM setups.

## Additional Note
The project is designed to be accessible in basic Windows environments without WSL2 or container runtime, broadening its usability.

## License

This project is licensed under the BSD 2-Clause "Simplified" License. For more details, see the LICENSE file in the repository.

## DEMO

Watch a setup demo here.
[![asciicast](https://asciinema.org/a/RsaQfY4CeZG25U4vwdLxYZhES.svg)](https://asciinema.org/a/RsaQfY4CeZG25U4vwdLxYZhES)

