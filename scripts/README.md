# Kubernetes kubectl plugin — kubeplugin

## Description

`kubeplugin` is a Bash-based kubectl plugin that retrieves CPU and memory usage statistics for Kubernetes resources.

The plugin uses the Kubernetes Metrics API through the `kubectl top` command.

## Requirements

- Kubernetes cluster
- kubectl
- Bash
- Metrics Server installed in the cluster

## Installation

Clone the repository:

```bash
git clone https://github.com/USERNAME/REPOSITORY.git
cd REPOSITORY
```

Create a directory for kubectl plugins:

```bash
mkdir -p ~/.local/bin
```

Install the plugin:

```bash
cp scripts/kubeplugin ~/.local/bin/kubectl-kubeplugin
chmod +x ~/.local/bin/kubectl-kubeplugin
```

Add the plugin directory to PATH:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

To make this change permanent:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Usage

```bash
kubectl kubeplugin <resource> <namespace>
```

### Examples

Get Pod resource statistics from kube-system:

```bash
kubectl kubeplugin pods kube-system
```

Get Pod statistics from default:

```bash
kubectl kubeplugin pods default
```

Get Pod statistics from monitoring:

```bash
kubectl kubeplugin pods monitoring
```

## Output format

The plugin displays resource statistics in the following format:

```text
Resource, Namespace, Name, CPU, Memory
```

Example:

```text
Resource   Namespace            Name                                          CPU        Memory
pods       kube-system           coredns-577d995dff-wqqlk                     5m         15Mi
pods       kube-system           local-path-provisioner-56c6584955-nzjqq      1m         8Mi
pods       kube-system           metrics-server-778c4649b4-tj94f             9m         24Mi
pods       kube-system           node-local-dns-bngl9                         5m         11Mi
pods       kube-system           svclb-traefik-681fa606-62vzq                 0m         0Mi
pods       kube-system           traefik-5d745cd6bf-vlr9q                     3m         24Mi
```

## Troubleshooting

If Metrics Server is unavailable, check its status:

```bash
kubectl get pods -n kube-system
```

Check resource metrics:

```bash
kubectl top pods -n kube-system
```

If the plugin is not detected:

```bash
kubectl plugin list
```

Ensure that `~/.local/bin` is included in your PATH.
