# Deploying MAS on a Single OpenShift Node (SNO) in Disconnected Environments

IBM Maximo Application Suite (MAS) is an integrated asset lifecycle management solution that streamlines the maintenance, inspection and reliability of your critical equipment and infrastructure by leveraging generative AI, advanced analytics and monitoring. Built on top of Red Hat OpenShift container platform, MAS can be hosted on-prem and in the cloud, or hosted as a managed service (SaaS).

While a typical MAS deployment for production or non-production involves multiple nodes for the OpenShift cluster, there are use cases where a single node OpenShift and MAS deployment makes economic sense, for example, running a MAS Manage locally for demo and learning purposes, or hosting it for use by a small working group. 

You can find OpenShift and MAS deployments on a single node from Red Hat and IBM documentation publicly available. However, deploying MAS on SNO in disconnected environments (also known as air gaped installation) is not a simple task. 

In this document, we will share the best practices, including some troubleshooting tips, on how to deploy MAS on a single node in disconnected environments. 

## A high-level overview of air-gaped installation

Unlike installations with Internet access, an air-gaped installation for OpenShift and MAS requires downloading or mirroring Red Hat and IBM container images and software operators to a local image registry and use them during installation. This results in a few extra steps:

1. Creating a local image registry, with a self-signed certificate
2. Mirroring all required images to the local image registry
3. Configuring the OpenShift cluster to use mirrored images

## A disconnected environment for OpenShift deployment

You will need at least two machines or hosts, and optionally a route with DHCP.

- The workstation or host

A Windows 10 or higher with Linux subsystem, Linux or MacBook with at least 1 TB storage. In our test, we used an Ubuntu host, Ubuntu 24.04.2 LTS. 

The workstation has Internet access and is connected to the target host on the same LAN with DHCP, vlan without DHCP, or using a cross-over cable.

- The target host where the OpenShift cluster will be deployed

The minimum configuration for a SNO environment ([OpenShift version 4.16](https://docs.redhat.com/en/documentation/openshift_container_platform/4.16/html/installing_on_a_single_node/preparing-to-install-sno)) is as follows.

* 8 vCPUs
* 16 GB of RAM
* 2 TB local storage

The target host is on the same network with the workstation and can communicate with the workstation. It has no Internet access.

- A route with DHCP. Without it, you will need to configure a DNS server on the workstation, resolving fully qualified domain names e.g. *.apps.maximo.localhost.com and api.maximo.localhost.com to IP addresses.

## Configuring a local DNS server on the workstation

This step is necessary when a router with DHCP is unavailable. 

## Create a local image registry on the workstation

...

### Generate a self-signed certificate with openssl

### Host a local image registry with podman or docker

## Install OpenShift on SNO

### Mirror Red Hat images to the local image registry

### Create install and machine configuration yaml files

### Download the RHEL Core (Live) iso image

## Create storage on SNO

## Install MAS using ansible playbooks

### Mirror MAS and Red Hat images to the local registry

### Configure MAS and Red Hat images 

### Install MAS Core

### Install MAS Manage

## Troubleshooting issues

### Red Hat cert manager operator failed to install

### Certificate invalid for the local image

### Images in the local registry are not used


## Acknowledgement

This document is a collaborative effort with two IBMers and co-authors, Kene Nwankwo and James Appleyard, who have been instrumental to resolving many technical issues during the project.


