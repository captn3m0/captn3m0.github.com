---
title: 'Kayak: Self-hosted Kubernetes cluster using Terraform Docker Provider and Bootkube'
layout: post
tags:
    - terraform
    - docker
    - terraform-provider-docker
    - bootkube
    - kayak
    - kubernetes
---

I manage my homeserver using the Terraform Docker Provider. While it is not quite as flexible as running Kubernetes, it does offer quite a lot of advantages and lets me get my hands dirty with Terraform. If you haven't worked with it, it lets Terraform talk to a Docker remote API and schedule docker containers easily. When I decided to work on bootstrapping my cluster with bootkube, the natural choice I had was to try to bring it up with the Terraform Docker Provider.

This turned out to be a very audacious goal, and was tricky to get working. The whole architecture, once the cluster is up, looks like this (middle-click to embiggen):

[![Home Server Kubernetes Block Diagram](/img/k8s.jpg)](/img/k8s.jpg)

The objectives are:

1. Run _everything_ as a Docker Container.
2. Make sure that the cluster is only exposed on the OpenVPN Network Interface.
3. No system level changes on the server, except for Docker API setup.

## Why is this a big deal?

-   This manages to run kubelet inside a docker container without using the `--containerized` flag.
-   There is no systemd/shell scripting involved. This is important because it moves all the configuration to terraform.

## The How of it

The walkthrough steps would be roughly:

1. [Get Docker API running on your server](https://success.docker.com/article/how-do-i-enable-the-remote-api-for-dockerd). If you're on CoreOS, you can use this [nice ignition module](https://registry.terraform.io/modules/captn3m0/docker-api/ignition/1.0.3) I wrote to avoid shell scripting.
1. [Setup this API against your local Terraform configuration.](https://www.terraform.io/docs/providers/docker/index.html)
1. Run [terraform-render-bootkube](https://github.com/poseidon/terraform-render-bootkube) from the [typhoon](http://typhoon.psdn.io/) project to generate the assets for the cluster. See [terraform config](https://git.captnemo.in/nemo/nebula/src/branch/kubernetes/kubernetes.tf#L69-L77).
1. Run [etcd](https://coreos.com/etcd/) as a container with a volume mount for the etcd-data. See [terraform module](https://git.captnemo.in/nemo/nebula/src/branch/kubernetes/modules/etcd/main.tf) and [usage](https://git.captnemo.in/nemo/nebula/src/branch/kubernetes/kubernetes.tf#L1-L20)
1. Run [kubelet] as a container with many volume mounts. See [terraform module](https://git.captnemo.in/nemo/nebula/src/branch/kubernetes/modules/kubelet/main.tf) and [usage](https://git.captnemo.in/nemo/nebula/src/branch/kubernetes/kubernetes.tf#L22-L39)
1. Run [bootkube start](https://github.com/kubernetes-incubator/bootkube) as a container with access to docker daemon. See [terraform module](https://git.captnemo.in/nemo/nebula/src/branch/kubernetes/modules/bootkube/main.tf) and [usage](https://git.captnemo.in/nemo/nebula/src/branch/kubernetes/kubernetes.tf#L41-L67)
1. Wait for the cluster to come up.

The primary challenges in this project were getting the kubelet and bootkube to run inside docker containers without complaining. It was made worse by the fact that kubelet's `--containerized` flag is no longer supported.

What helped me along the way was:

1. Reverse engineering the [kubelet-wrapper](https://github.com/coreos/coreos-overlay/blob/master/app-admin/kubelet-wrapper/files/kubelet-wrapper) script from Core OS to figure out the correct mounts for kubelet. However, kubelet-wrapper runs using [`rkt`](https://coreos.com/rkt/) and not docker, which changes a lot of things.
2. Looking up typhoon's usage of the terraform-render-bootkube module to figure out what files are expected in what locations by bootkube. Some files have 3 different locations on disk, and it gets quite confusing.
3. Checking error logs for kubelet or the control plane components that don't come up.
4. Bouncing off ideas against [Rahul] and asking on kubernetes slack for help.

I'll be wrapping this into a neatly published package on the Terraform registry soon. But meanwhile, if you're looking to emulate this, note that it requires a [slightly patched version of the terraform-docker-provider](https://github.com/captn3m0/terraform-provider-docker/commit/f83bd43fd9618ce22353484c924b912e35b38718) which adds support for shared volume mounts (necessary for kubelet).
