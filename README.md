# Demo - Gathering and Preparing data onPrem with OpenShift AI

This project contains the configurations to provide infrasctructure, on OpenShift, that supports ML and AI workloads for a blueshield demo.  The demo involves gathering unstructured pdfs and using labelstudio (with tesseract) to structure data from the pdfs into structured data.  Structured data will be stored in a vector DB (postgres).  Data will be pulled by a pipeline from an ARO cloud configuration.  

The demo demonstrates the value of using OpenShift (onPrem) to gather/curate onPrem data which is then used by the ARO cloud instance for model training.

***This repo is currently subject to frequent, breaking changes!***

## Prerequisites

- OpenShift 4.8+
  - role: `cluster-admin` - for all [demo](demos) or [cluster](clusters) configs
  - role: `self-provisioner` - for namespaced components

[Red Hat Demo Platform](https://demo.redhat.com) Options (Tested)

- <a href="https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.sandbox-ocp.prod&utm_source=webapp&utm_medium=share-link" target="_blank">AWS with OpenShift Open Environment</a>
  - 1 x Control Plane - `m6.4xlarge`
  - 0 x Workers - `m6.2xlarge`
- <a href="https://demo.redhat.com/catalog?item=babylon-catalog-prod/sandboxes-gpte.ocp4-single-node.prod&utm_source=webapp&utm_medium=share-link" target="_blank">One Node OpenShift</a>
  - 1 x Control Plane - `m6.4xlarge`
- <a href="https://demo.redhat.com/catalog?item=babylon-catalog-prod/community-content.com-mlops-wksp.prod&utm_source=webapp&utm_medium=share-link" target="_blank">MLOps Demo: Data Science & Edge Practice</a>

### Tools

The following cli tools are required:

- `bash`, `git`
- `oc` - Download [mac](https://formulae.brew.sh/formula/openshift-cli), [linux](https://mirror.openshift.com/pub/openshift-v4/clients/ocp), [windows](https://mirror.openshift.com/pub/openshift-v4/clients/ocp/stable/openshift-client-windows.zip)
- `kubectl` (optional) - Included in `oc` bundle
- `kustomize` (optional) - Download [mac](https://formulae.brew.sh/formula/kustomize), [linux](https://github.com/kubernetes-sigs/kustomize/releases)

NOTE: `bash`, `git`, and `oc` are available in the [OpenShift Web Terminal](https://docs.openshift.com/container-platform/4.12/web_console/web_terminal/installing-web-terminal.html)

The following are used to encrypt secrets and are optional:

- `age` - [Info](https://github.com/FiloSottile/age)
- `sops` - [Info](https://github.com/getsops/sops)

## Bootstrapping a Cluster

1. Verify you are logged into your cluster using `oc`.
1. Clone this repository

To a local environment

```sh
oc whoami
git clone < repo url >
```

Use an [OpenShift Web Terminal](https://docs.openshift.com/container-platform/4.12/web_console/web_terminal/installing-web-terminal.html)

```
YOLO_URL=https://raw.githubusercontent.com/codekow/demo-ai-gitops-catalog/main/scripts/library/term.sh
. <(curl -s "${YOLO_URL}")
term_init

# make custom web terminal persistent
apply_firmly bootstrap/web-terminal
```

NOTE: open a new terminal to activate new configuration

### Cluster Quick Start for OpenShift GitOps

Basic cluster config

```sh
# load functions
. scripts/functions.sh

# setup an enhanced web terminal on a default cluster
# alt cmd: until oc apply -k bootstrap/web-terminal; do : ; done
apply_firmly bootstrap
```