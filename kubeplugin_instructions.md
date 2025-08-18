# kubeplugin

## Overview

`kubeplugin` is a simple **Bash plugin for **`` that retrieves CPU and memory usage statistics for Kubernetes pods.

It can display:

- All pods in a namespace
- A specific pod in a namespace

The output format is:

```
Resource: pods, Namespace: <namespace>, Name: <pod_name>, CPU: <cpu_usage>, Memory: <memory_usage>
```

This plugin is useful for quick monitoring of pod resource usage without installing additional tools.

---

## Prerequisites

- Kubernetes cluster access (`kubectl` configured)
- Bash shell

---

## Usage

### 1. Show all pods in a namespace

```bash
./kubeplugin <namespace>
```

Example:

```bash
./kubeplugin kube-system
```

Output:

```
Resource: pods, Namespace: kube-system, Name: coredns-5644d7b6d9-abcde, CPU: 5m, Memory: 12Mi
Resource: pods, Namespace: kube-system, Name: etcd-minikube, CPU: 10m, Memory: 30Mi
...
```

### 2. Show a specific pod

```bash
./kubeplugin <namespace> <pod_name>
```

Example:

```bash
./kubeplugin kube-system coredns-5644d7b6d9-abcde
```

Output:

```
Resource: pods, Namespace: kube-system, Name: coredns-5644d7b6d9-abcde, CPU: 5m, Memory: 12Mi
```

---

## Notes

- If no resources are found, nothing is displayed.
- This plugin uses `kubectl top pods`, so metrics-server must be installed in your cluster.
- The plugin can be easily modified to include more resource types or namespaces.

