# README: quick-dev-vagrant

## Overview
This project simplifies creating a DevOps environment with Vagrant, automating the setup of virtual machines (VMs) to mirror development, testing, or production setups easily.
Leveraging a `boxes.yml` file, it employs a configuration-driven method for VM provisioning and includes a controller VM with Ansible, eliminating the need for local Ansible installations.
Originally developed for personal use, this project is now shared for anyone with similar needs.

Vagrant is an open-source tool that facilitates the building and managing of virtualized development environments.
For more details, visit [Vagrant's official website](https://www.vagrantup.com/).

### Important Note

This is the first release, only tested on Apple Silicon with Parallels Desktop 19 Pro. This repository is released following the "release early, release often" principle to gather feedback and improve continuously.

> "Release early, release often."
>
> - Eric S. Raymond, ["The Cathedral and the Bazaar"](http://www.catb.org/~esr/writings/cathedral-bazaar/cathedral-bazaar/)

## Prerequisites
Before you begin, ensure you have the following installed on your system:
- Vagrant
- VirtualBox or Parallels (depending on your provider preference)

**Note:** Ansible is not required to be installed on your local machine. 
The "controller" VM provisioned by this setup will include Ansible for all configuration management tasks.

### Quickstart

1. Install [Vagrant](https://www.vagrantup.com/downloads) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
2. Clone this repository and navigate to it.
3. Run `vagrant up` to provision and start your VM.

This will use the default configuration from `boxes.yml` to get your environment up and running quickly.

## Tested Environment

Ensure your setup matches or is compatible with the environments listed below to avoid any potential issues. 
If you've successfully run the system with a different configuration, please provide details to help expand this list.

- **Test Environment 1:**
  - **OS:** macOS 14.3.1, Sonoma
  - **Arch**: ARM64, Apple Silicon M1
  - **Vagrant Version:** 2.4.1
  - **Parallels Version:** 19.3.0 Pro

## Limitations

Currently, the setup and configurations provided in this project have only been tested with Debian-based Vagrant boxes.
While there is potential for compatibility with other Unix-like systems, these have not been officially tested, and users may encounter issues or require additional configuration steps.

Key points include:
- The project is optimized for Debian-based distributions.
- Compatibility with non-Debian-based boxes, such as those from the Fedora, CentOS, or openSUSE families, has not been evaluated.
- Users attempting to use other distributions should be prepared for troubleshooting and potentially contributing fixes to enhance compatibility.

We welcome feedback and contributions from users who explore this setup with other operating systems, as it can help us improve and expand the project's reach.


## Installation
1. Clone this repository to your local machine.
2. Navigate to the cloned directory.
3. Ensure `boxes.yml` is configured according to your environment setup needs.

The cloned repository is accessible from inside the VM under `/vagrant`. 
A `requirements.txt` is provided as an example for Python dependencies. 
To create a Python virtual environment and install the dependencies, run the following commands inside the VM:

```
cd /vagrant`
python3 -m venv venv 
source venv/bin/activate 
pip install -r requirements.txt
```

### Future Improvements / TODO

This section outlines potential future improvements and features for the project. It serves as a roadmap for development and an invitation for contributors interested in enhancing the project.

- **Environment-specific Configuration Directories:**
  - Create a `environments/` directory at the project root.
  - Inside `environments/`, have subdirectories for each specific environment tested, such as `tomcat-testing/`.
  - Each environment directory should contain its own `boxes.yml` and the necessary Ansible playbooks for provisioning the VMs within that environment.

- **Enhanced Environment Flexibility:**
  - Develop the capability to replace the "controller" VM with a container in environments where this would be beneficial, enhancing flexibility and reducing overhead.
  - Introduce the option to mix containers and VMs within a single environment setup. This would allow for more complex and varied setups, combining the strengths of both containers and virtual machines.
  - see also the [Additional Note](#additional-note) section.

These improvements aim to make the project more modular, flexible, and suitable for a wider range of development, testing, and production scenarios. Contributions towards achieving these goals are highly welcome, as they will help in evolving the project to meet diverse user needs and preferences.

### Additional Note

While provisioning environments using solely Ansible could simplify the process, this project aims to be accessible and functional even in basic Windows environments without the need for WSL2 or a container runtime. This consideration is particularly important for scenarios where users are on platforms like Windows Server 2019, which does not support Linux VMs in Docker. Ensuring compatibility with such environments broadens the usability of the project, allowing it to serve a wider audience who might not have access to or prefer not to use more complex setup requirements.

For more details on WSL2, visit [Microsoft's official documentation](https://docs.microsoft.com/en-us/windows/wsl/about).


## License
This project is licensed under the [2-Clause BSD License](https://opensource.org/licenses/BSD-2-Clause). 
A copy of the license is included in the repository.

This version corrects the nested code block and ensures clarity and consistency throughout the document.

## DEMO

[![asciicast](https://asciinema.org/a/RsaQfY4CeZG25U4vwdLxYZhES.svg)](https://asciinema.org/a/RsaQfY4CeZG25U4vwdLxYZhES)
