# Private Cloud Template Resources

## Overview 

This repository provides templates and useful snippets of templates for building OpenStack templates for deploying clusters on private cloud.

The repository is setup with the following directories:
- `snippets/` - A directory for useful snippets of templates that can be stitched together to create full templates
- `templates/` - Fully written templates ready to be used

This repository supposes that the [Flight Solo](https://www.openflighthpc.org/latest/solo/) image is being used as the image source for all nodes. This is because it provides necessary hooks and configuration for the various user-data scripts supplied for automatic configuration.

## Snippets

### Usage

The snippets aren't just ready to be copied/pasted but instead provide some initial structure for various resources (including parameters, etc). Due to this, when constructing a template, the parameters will need to be manually merged for any of the snippets which are being combined. Additionally, automated setup for various cluster types will need to be updated.

### Network and Security

This snippet provides the entire network and security group for a functional cluster along with internet gateways.

### Gateway with Automatic Shared Storage Mount

This snippet provides a server that automatically mounts a 100GB storage disk to `/export` which will be exported over NFS (if a multinode cluster is configured with `flight-profile`). 

For more information on various cloud-init data that can be provided to the `/opt/flight/cloudinit.in` see the [OpenFlight docs](https://www.openflighthpc.org/latest/docs/flight-solo/understand-solo/user-data/).

### Compute Node

This snippet provides a basic node template. It has NODENAME and NODEIP text which should be replaced (e.g. with `sed` replacing `NODENAME` with `node01` and `NODEIP` with `1` (because the IP can't end `.01`)) when added to a template. This makes it slightly easier to generate a bunch of similar compute nodes to be added to a template.

## Templates

### SLURM Team Edition

This template launches a gateway, infrastructure and 5 compute nodes. They are automatically configured with IPA for multi-user access management and shared storage of 100GB shared over the configured NFS directories.

### JupyterLab Jumpstart

This template launches a gateway node that automatically configures a Jupyter Lab environment accessible through web suite on the external IP of the node. It comes with 100GB of local storage across the whole system. 

### Container Cruncher Small 

This template launches a gateway node and 2 compute nodes. The cluster runs a Kubernetes cluster configuration for the user `flight` with shared storage of 100GB shared over the configured NFS directories.

### Container Cruncher Medium

This template launches a gateway node and 5 compute nodes. The cluster runs a Kubernetes cluster configuration for the user `flight` with shared storage of 500GB shared over the configured NFS directories.

### Container Cruncher Large 

This template launches a gateway node and 10 compute nodes. The cluster runs a Kubernetes cluster configuration for the user `flight` with shared storage of 1TB shared over the configured NFS directories.

### CFD Jumpstart

This template launches a gateway node and 5 compute nodes. The cluster runs a SLURM environment and preinstalls OpenFOAM 22.12 and OpenMPI to provide a working CFD environment for job workflows and shared storage of 1TB over the configured NFS directories.

