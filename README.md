# Container Management System using Bash Script

## Project Overview

This project, **Container Management System using Bash Script**, is a minimalistic container manager developed from scratch using Bash scripting. It showcases the fundamental Linux concepts of namespaces, chroot, and networking, without relying on established container management tools like Docker or Kubernetes.

## Table of Contents
- [Introduction](#introduction)
- [Project Objective](#project-objective)
- [Prerequisites](#prerequisites)
- [Approach](#approach)
  - [Key Functionalities](#key-functionalities)
- [Implementation Details](#implementation-details)
  - [Utility Functions](#utility-functions)
  - [Container Management](#container-management)
  - [Networking](#networking)
- [Challenges and Solutions](#challenges-and-solutions)
- [Testing and Validation](#testing-and-validation)
- [Future Enhancements](#future-enhancements)
- [Conclusion](#conclusion)
- [Repository](#repository)

## Introduction

Containers are crucial for modern software deployment due to their lightweight virtualization. This project implements a basic container management system in Bash, capable of building, running, and managing containers with a focus on simplicity and educational value.

## Project Objective

The main objective is to develop a Bash-based container manager that can:
- Build container images.
- Run containers in isolated environments.
- Set up networking between containers and the host.
- Execute programs within running containers.
- Facilitate peer-to-peer communication between containers.

## Prerequisites

Before running the script (`conductor.sh`), ensure the following requirements are met:
- **Operating System**: Linux-based OS with root privileges.
- **Required Tools**: `debootstrap`, `ip`, `iptables`, `nsenter`, `chroot`.
- **Filesystem Directories**: The script creates necessary directories for storing container images, runtime files, and extras if they do not exist.

## Approach

The project utilizes various Linux features to manage containers:

### Key Functionalities
- **Building Containers**: Creates Debian-based container images using `debootstrap`.
- **Running Containers**: Launches containers with isolated namespaces and mounts necessary filesystems.
- **Stopping Containers**: Terminates running containers and cleans up resources.
- **Executing Programs in Containers**: Runs commands inside containers using `nsenter`.
- **Networking Setup**: Configures container networking with `veth` pairs, NAT, and routing.
- **Peer-to-Peer Communication**: Enables direct communication between containers via `iptables` rules.

## Implementation Details

### Utility Functions
- `die()`: Prints an error message and exits the script.
- `check_prereq()`: Checks for root permissions and required tools.
- `get_next_num()`: Retrieves the next available container identifier.
- `wait_for_dev()`: Waits for the network interface to be ready.

### Container Management
- `build()`: Builds a Debian-based container image using `debootstrap`.
- `run()`: Runs a container with isolated namespaces and necessary mounts.
- `stop()`: Stops a running container and cleans up resources.
- `exec()`: Executes a program within a running container using `nsenter`.
- `images()`: Displays available container images.
- `remove_image()`: Deletes a container image.

### Networking
- `addnetwork()`: Sets up networking for containers using `veth` pairs, NAT, and routing.
- `peer()`: Configures peer-to-peer communication between two containers.

## Challenges and Solutions

- **Namespace Isolation**: Achieved through `unshare` and mounting necessary filesystems within containers.
- **Networking**: Handled via `veth` pairs, IP configuration, and `iptables` rules for NAT and routing.

## Testing and Validation

The script was tested on a Linux-based system with root privileges. The following were validated:
- Container Creation: Successfully built and stored Debian-based container images.
- Container Execution: Containers ran with isolated namespaces and could execute basic commands.
- Networking: Containers communicated with the host and each other, with NAT enabling internet access
