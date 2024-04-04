# Demo - Gathering and Preparing data onPrem with OpenShift AI

This project contains the configurations to provide infrasctructure, on OpenShift, that supports ML and AI workloads for a blueshield demo.  The demo involves gathering unstructured pdfs and using labelstudio (with tesseract) to structure data from the pdfs into structured data.  Structured data will be stored in a vector DB (postgres).  Data will be pulled by a pipeline from an ARO cloud configuration.  

The demo demonstrates the value of using OpenShift (onPrem) to gather/curate onPrem data which is then used by the ARO cloud instance for model training.

_This repo is currently subject to frequent, breaking changes!_

## Prerequisites

### OpenShift 4.8+

- role: cluster-admin for all demo or cluster configs
- role: self-provisioner - for namespaced components

### Red Hat Demo Platform Options (Tested)

...

### The following cli tools are required

- bash, git
- oc - Download mac, linux, windows
- kubectl (optional) - Included in oc bundle
- kustomize (optional) - Download mac, linux

NOTE: bash, git, and oc are available in the OpenShift Web Terminal

### Tools

The following are used to encrypt secrets and are optional:

- age - Info
- sops - Info
  
### Bootstrapping a Cluster

1. Verify you are logged into your cluster using oc
2. Clone this repository

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
apply_firmly bootstrap/web-terminal
```
