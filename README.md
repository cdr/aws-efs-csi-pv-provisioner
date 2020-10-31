# AWS EFS CSI PV provisioner

Kubernetes CSI driver to dynamically provisions Persistent Volumes (PVs) in response to user-requested Persistent Volume Clains (PVCs). Each PV / PVC is a subdirectory on a single, cluster-wide EFS file system. Works in conjunction with the [AWS EFS CSI driver](https://github.com/kubernetes-sigs/aws-efs-csi-driver).

## Installation

1. Create an EFS filesystem and mount targets for your cluster.
2. Install the [AWS EFS CSI driver](https://github.com/kubernetes-sigs/aws-efs-csi-driver) with a corresponding `StorageClass` called `efs-sc`.
3. Build a Docker image with the Dockerfile in this repository and push it into a repository. Put the image URL into `deploy/deployment.yaml`.
4. Put your EFS file system IDs into `deploy/deployment.yaml` and `deploy/pv.yaml`.
5. (Optional) Modify the desired mount options in `deploy/pv.yaml` and `deploy/sc.yaml` (e.g. to disable TLS and IAM if not needed).
6. Apply the manifests: `kubectl -n kube-system apply -f deploy/`


## "How it works" overview diagram

![](docs/overview.svg)

## TODOs

* create CI to build and push Docker image
* provide Helm chart
* potentially integrate into AWS EFS CSI driver
