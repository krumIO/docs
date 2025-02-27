---
sidebar_position: 9
keywords:
  - Harvester
  - harvester
  - Rancher
  - rancher
  - Developer Mode Installation
Description: Developer mode (dev mode) is intended to be used for testing and development purposes.
---

# Developer Mode Installation

Developer mode (dev mode) is intended to be used for testing and development purposes.

This video shows the dev mode installation.

<iframe width="950" height="475" src="https://www.youtube.com/embed/TG0GaAD_6J4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Requirements

- We assume **Multus** is installed across your cluster and a corresponding `NetworkAttachmentDefinition` CRD was created.
- If you are using an [RKE](https://rancher.com/docs/rke/latest/en/) cluster, please ensure the `ipv4.ip_forward` is enabled for the CNI plugin so that the pod network works as expected, related issue: [#94](https://github.com/harvester/harvester/issues/94).

## Install as an App

Harvester can be installed on a Kubernetes cluster in the following ways:

- Install with the [Helm](https://helm.sh/) CLI
- Install as a Rancher catalog app, in which case the [harvester/harvester](https://github.com/harvester/harvester) repo is added to the Rancher Catalog as a Helm `v3` app

Please refer to the Harvester [Helm chart](https://github.com/harvester/harvester/blob/master/deploy/charts/harvester/README.md) for more details on installing and configuring the Helm chart.

### Requirements

The Kubernetes node must have hardware virtualization support.

To validate the support, use this command:

```bash
cat /proc/cpuinfo | grep vmx
```

### Option 1: Install using Helm

1. Clone the GitHub repository:
   ```bash
   git clone https://github.com/harvester/harvester.git --depth=1
   ```

1. Go to the Helm chart:
   ```bash
   cd harvester/deploy/charts
   ```

1. Install the Harvester chart with the following commands:
   ```bash
   ### To install the chart with the release name `harvester`:

   ## Create the target namespace
   kubectl create ns harvester-system

   ## Install the chart to the target namespace
   helm install harvester harvester \
   --namespace harvester-system \
   --set longhorn.enabled=true
   ```

### Option 2: Install using Rancher

!!! tip
      You can create a testing Kubernetes environment in Rancher using the Digital Ocean cloud provider. For details, see [this section](#digital-ocean-test-environment).

1. Add the Harvester repo `https://github.com/harvester/harvester` to your Rancher catalogs by clicking **Global > Tools > Catalogs**.
1. Specify the URL and name. Set the branch to `stable` if you need a stable release version. Set the `Helm version` to be `Helm v3`.
   ![harvester-catalog.png](harvester-catalog.png)
1. Click **Create**.
1. Navigate to your project-level `Apps.`
1. Click `Launch` and choose the Harvester app.
1. (Optional) You can modify the configurations if needed. Otherwise, use the default options.
1. Click **Launch** and wait for the app's components to be ready.
1. Click the `/index.html` link to navigate to the Harvester UI, as shown in the figure below:
   ![harvester-app.png](harvester-app.png)

### Digital Ocean Test Environment

[Digital Ocean](https://www.digitalocean.com/) supports nested virtualization by default.

You can create a testing Kubernetes environment in Rancher using the Digital Ocean cloud provider.

We recommend using the `8 core, 16 GB RAM` node, which will have nested virtualization enabled by default.

This screenshot shows how to create a Rancher node template that would allow Rancher to provision such a node in Digital Ocean:

![do.png](do.png)

For more information on how to launch Digital Ocean nodes with Rancher, refer to the [Rancher documentation.](https://rancher.com/docs/rancher/v2.x/en/cluster-provisioning/rke-clusters/node-pools/digital-ocean/)
