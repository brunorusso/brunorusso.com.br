---
title: "The Achilles' Heel of KubeVirt: Why Storage and Testing Matter"
author: "Bruno Russo"
date: 2026-10-24 22:40 -0300
categories: ["Arquitetura", "Transformação Digital", "Governança", "k8s"]
tags: ["Open Source", "Linux", "Kubernetes", "kubevirt"]
ping: true
math: true
mermaid: true
image: 
    path: https://www.brunorusso.com.br/assets/2026/k8s-and-vms-kubevirt.jpeg
    alt: "Ilustração 3D em tons claros representando a integração de Máquinas Virtuais (VM) em um cluster Kubernetes (K8S) com ícones de infraestrutura."
---

A few months ago, I began an in-depth study on virtualization based on [kubevirt](https://kubevirt.io/).

You might be asking yourself: why focus on virtualization in the age of cloud computing, let alone on top of Kubernetes?

The answer is straightforward. Most companies still maintain huge fleets of virtual machines and need a robust platform to operate them. While VMware by Broadcom has traditionally dominated the market share, organizations are increasingly looking for powerful, cost-effective alternatives.

KubeVirt emerges as an excellent solution to fill this gap.


**A brief explanation of KubeVirt**

> KubeVirt technology addresses the needs of development teams that have adopted or want to adopt [Kubernetes](https://kubernetes.io/) but possess existing Virtual Machine-based workloads that cannot be easily containerized. More specifically, the technology provides a unified development platform where developers can build, modify, and deploy applications residing in both Application Containers as well as Virtual Machines in a common, shared environment.
> 
> Benefits are broad and significant. Teams with a reliance on existing virtual machine-based workloads are empowered to rapidly containerize applications. With virtualized workloads placed directly in development workflows, teams can decompose them over time while still leveraging remaining virtualized components as is comfortably desired.

KubeVirt is an open-source project, and its adoption is growing rapidly month by month. Many features have been released, and today, when comparing core virtualization capabilities, KubeVirt stands toe-to-toe with VMware. While you might need a specific feature to address a unique edge case, the overall virtualization ecosystem is highly robust.

Running a virtual machine is just a small part of the broader ecosystem. You also need hardware (CPU and memory), networking, storage, backup solutions, and more. All these components must work together seamlessly. Therefore, thoroughly testing this entire stack is essential.   

While looking to create a custom testing solution for this, I discovered a tool developed by Pure Storage called Virtbench.

---
## What is Virtbench created by Pure Storage?

Virtbench is a tool created by Pure Storage designed to determine the storage and performance requirements of a workload before it goes into production. Simply put, it helps estimate the necessary storage space and IOPS to avoid bottlenecks once a workload is deployed.

> A comprehensive, vendor-neutral performance testing toolkit for KubeVirt virtual machines running on OpenShift Container Platform (OCP) or any Kubernetes distribution with KubeVirt.
> This suite provides automated performance testing tools to measure and validate KubeVirt VM provisioning, boot times, network readiness, and failure recovery scenarios. It's designed for production environments running OpenShift Virtualization or KubeVirt with any CSI-compatible storage backend.

The 10 tests available are:

1. VM Creation (DataSource Clone) - Tests VM creation using KubeVirt DataSource cloning for efficient VM provisioning.
    - **Use Case**: Measure VM provisioning performance with your storage backend.

2. Boot Storm Testing - Mass simultaneous VM startup test to validate concurrent startup performance, storage/network/compute bottlenecks, and disaster recovery RTO.
    - **Use Case**: Validate cluster behavior during power-outage recovery, post-maintenance cold starts, or any scenario where many VMs start at once.

3. Live Migration Testing - Tests VM live migration with existing VMs or by creating new VMs across different scenarios.
    - **Use Case**: Validates migration performance for node maintenance, load balancing, and disaster recovery scenarios.

4. Chaos Benchmark Testing - Tests cluster resilience by running concurrent chaos operations including VM creation, volume resize, volume clone, VM restart, and snapshots.
    - **Use Case**: Stress-test the cluster with concurrent operations, validate volume cloning, and measure performance under load.

5. Failure and Recovery Testing - Tests VM recovery time after simulated node failures using Fence Agents Remediation (FAR).
    - **Use Case**: Validates high availability and disaster recovery capabilities.

6. Cluster Validation (Openshift Only) - Validates that your OpenShift cluster is properly configured and ready to run KubeVirt performance tests.
    - **Use Case**: Pre-flight checks before running benchmarks.


7. FIO Storage I/O Benchmark - Tests storage I/O performance by running FIO benchmarks across multiple VMs in parallel.
    - **Use Case**: Measure storage IOPS, bandwidth, and latency under various workload patterns.

8. Elbencho Storage Benchmark - Runs the elbencho storage micro-benchmark across multiple VMs to measure file-system level throughput and latency.
    - **Use Case**: Compare storage performance for file-based workloads alongside FIO results.

9. VM Operations (Day-2) - Day-2 lifecycle operations for benchmarking and validation: drain nodes, rebalance VMs, snapshot in batches, run blkdiscard, and power VMs on/off.
    - **Use Case**: Exercise VM lifecycle paths individually or as building blocks for larger test plans.

10. Disk Operations (Hotplug/Coldplug) - Tests disk hotplug (attach to running VM) and coldplug (attach to stopped VM, then boot) performance, with optional in-VM validation that the disk appears.
    - **Use Case**: Measure disk attach/detach times and verify disks become usable inside running and stopped VMs.


---
## My impression about tests with Virtbench

> Important! Run these tests in a non-production environment. Some tests create heavy concurrency on the CPU, disk I/O, and other critical cluster resources.

I tested Virtbench with KubeVirt version 2.0, and the installation process was very simple. For more information about the installation, refer to the official documentation at: https://portworx.github.io/kubevirt-benchmark/install/.

In my case, I chose to perform the following tests:

- VM Creation (DataSource Clone)
- Boot Storm Testing
- Live Migration Testing
- Chaos Benchmark Testing
- FIO Storage I/O Benchmark
- VM Operations (Day-2)

All tests passed successfully, and no issues were detected. What makes these benchmarks particularly interesting is the ability to execute multiple operations concurrently. You can simultaneously create several virtual machines, take snapshots, resize disks, and much more, truly validating how your infrastructure handles the load.

## What is more important than Virtbench?

In my opinion, when dealing with a KubeVirt-based virtualization environment, the Achilles' heel is always the storage subsystem.

We must remember that Kubernetes was originally designed for—and is predominantly used by—stateless applications, meaning that persistent storage is often an afterthought. While storage is certainly part of the ecosystem, the vast majority of containerized applications do not demand high-end storage arrays.

> The term "high-end storage" refers to enterprise-grade, ultra-high-performance storage architectures.

Most enterprise organizations already maintain high-end storage in their environments, traditionally connected to physical servers via standard SAN (Storage Area Network) architectures.

Therefore, to bridge this enterprise storage technology with Kubernetes, you rely on a CSI Driver provided by the storage vendor.

> A CSI Driver (Container Storage Interface Driver) is a plugin that connects external storage systems (such as cloud disks, NAS, SAN, or file storage) to container orchestrators, most notably Kubernetes.

The CSI Driver is a simple container (or in many cases, a Pod) running in the environment.

Given the importance of storage and how we connect it to Kubernetes, it is necessary to understand that:


1. **Create a disk** – all operations to create a disk are handled by the CSI Driver.
2. **Delete a disk** – all operations to delete a disk are handled by the CSI Driver.
3. **Resize a disk** – all operations to resize a disk are handled by the CSI Driver.
4. **Clone a disk** – all operations to clone a disk are handled by the CSI Driver.
5. **Take a Snapshot** – all operations to snapshot a disk are handled by the CSI Driver.
6. **Attach a disk to a virtual machine** – all operations to attach a disk are handled by the CSI Driver.

The list above might sound repetitive, but it is crucial to understand the **real importance** of the CSI Driver.

Running Virtbench gives you a landscape view of the cluster, which is very important. However, understanding the behavior of the CSI Driver is essential to see how these six operations are executed and what happens under the hood.

When evaluating the CSI Driver, it is important to:

- Monitor the CSI Driver container's performance metrics during each specific operation.
- Analyze the CSI Driver logs. Tracing these logs lets you validate exactly how it behaves step-by-step. To make parsing this data easier, I highly recommend using an LLM.
- Test the driver's behavior against the specific, real-world scenarios present in your environment.

Another crucial point regarding the CSI Driver is the absolute necessity of reading—and rereading—the official vendor documentation. This is critical because its operational model differs significantly from traditional virtualization platforms. Moreover, it is quite common to find that a CSI Driver lacks certain advanced features you would normally have when manually provisioning a LUN, for instance. Because of this gap, thoroughly reviewing the documentation is essential.


## My conclusion

If you are considering adopting KubeVirt as your virtualization platform, you are definitely on the right track. I consider KubeVirt to be a highly stable and mature system, fully capable of supporting the vast majority of enterprise environments.

However, if relying on a pure upstream open-source project feels too risky for your organization, you can always opt for enterprise-grade solutions backed by major vendors, such as [Red Hat OpenShift Virtualization](https://www.redhat.com/en/technologies/cloud-computing/openshift/virtualization) or [SUSE Harvester](https://www.suse.com/products/rancher/virtualization/).