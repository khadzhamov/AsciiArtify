# AsciiArtify — Kubernetes Local Development Environment

## 1. Project Overview

AsciiArtify is a startup project focused on developing an application that converts images into ASCII art using Machine Learning.

The development team needs a local Kubernetes environment for application development, testing, deployment, and CI/CD integration.

The purpose of this document is to compare three tools for local Kubernetes development:

- Minikube
- Kind (Kubernetes IN Docker)
- K3d (K3s in Docker)

## 2. Comparison of Main Characteristics

| Criteria | Minikube | Kind | K3d |
| --- | --- | --- | --- |
| Purpose | Local development and learning | Kubernetes testing and CI | Lightweight development |
| Kubernetes distribution | Upstream Kubernetes | Upstream Kubernetes | K3s |
| Operating systems | Linux, macOS, Windows | Linux, macOS, Windows | Linux, macOS, Windows |
| Architecture | AMD64, ARM64 | AMD64, ARM64 | AMD64, ARM64 |
| Runtime | Docker, containerd, CRI-O, VM | Docker, Podman | Docker |
| Automation | CLI, profiles, addons | CLI, YAML | CLI, YAML |
| Dashboard | Available | Manual installation | Manual installation |
| Ingress | Addon | Manual installation | Traefik |
| LoadBalancer | minikube tunnel | Additional configuration | ServiceLB |
| Monitoring | Metrics Server, addons | External tools | K3s components |
| Prometheus / Grafana | Helm installation | Helm installation | Helm installation |
| Cluster management | CLI, kubectl, Dashboard | CLI, kubectl | CLI, kubectl |
| Multi-node support | Yes | Yes | Yes |
| Multi-control-plane | Supported configurations | Yes | Yes |
| Multiple clusters | Profiles | Named clusters | Named clusters |
| CI/CD integration | Good | Excellent | Excellent |
| Deployment speed | Fast | Very fast | Very fast |
| Resource consumption | Medium | Low | Low |
| Documentation | Excellent | Excellent | Good |
| Community support | Large | Very large | Active |

## 3. Advantages and Disadvantages

### Minikube

**Advantages:**

- Easy installation and configuration.
- Built-in Kubernetes Dashboard.
- Many useful addons.
- Supports multi-node clusters.
- Supports different drivers and runtimes.
- Excellent documentation.

**Disadvantages:**

- Higher resource consumption compared to Kind and K3d.
- Some features require additional configuration.
- Not intended for production workloads.

Documentation: https://minikube.sigs.k8s.io/docs/

### Kind

**Advantages:**

- Uses upstream Kubernetes.
- Very fast cluster creation.
- Supports multiple control-plane and worker nodes.
- Excellent CI/CD integration.
- Convenient YAML-based configuration.

**Disadvantages:**

- No built-in Dashboard.
- Ingress and LoadBalancer require additional configuration.
- Requires a container runtime.

Documentation: https://kind.sigs.k8s.io/

### K3d

**Advantages:**

- Very fast cluster creation.
- Low resource consumption.
- Supports multi-node clusters.
- Convenient local registry integration.
- Traefik and ServiceLB available through K3s.

**Disadvantages:**

- Uses K3s instead of upstream Kubernetes.
- Some Kubernetes components differ from standard distributions.
- Requires Docker.

Documentation: https://k3d.io/

## 4. Scalability Comparison

All three tools support multi-node clusters and can be used for local scalability testing.

| Feature | Minikube | Kind | K3d |
| --- | --- | --- | --- |
| Single-node cluster | Yes | Yes | Yes |
| Multi-node cluster | Yes | Yes | Yes |
| Multiple control-plane nodes | Supported | Yes | Yes |
| Multiple independent clusters | Yes | Yes | Yes |
| Kubernetes topology testing | Good | Excellent | Excellent |
| Production replacement | No | No | No |

**Summary:**

- Minikube is suitable for learning and small multi-node environments.
- Kind is excellent for testing Kubernetes topologies.
- K3d is suitable for lightweight multi-node development environments.

## 5. Monitoring and Cluster Management

| Component | Minikube | Kind | K3d |
| --- | --- | --- | --- |
| Kubernetes Dashboard | Addon | Manual | Manual |
| Metrics Server | Addon | Manual | Depends on configuration |
| Prometheus | Helm | Helm | Helm |
| Grafana | Helm | Helm | Helm |
| Cluster management | CLI, kubectl, Dashboard | CLI, kubectl | CLI, kubectl |

Prometheus and Grafana can be installed on all three platforms using Helm charts.

## 6. Evaluation Matrix

The following matrix evaluates the tools according to the initial requirements of AsciiArtify.

Scores range from 1 (poor) to 5 (excellent).

| Criteria | Weight | Minikube | Kind | K3d |
| --- | ---: | ---: | ---: | ---: |
| Ease of use | 25% | 5 | 4 | 5 |
| Built-in functionality | 20% | 5 | 3 | 4 |
| Scalability testing | 15% | 4 | 5 | 5 |
| Resource efficiency | 15% | 3 | 5 | 5 |
| Documentation and community | 15% | 5 | 5 | 4 |
| CI/CD integration | 10% | 4 | 5 | 5 |
| **Weighted score** | **100%** | **4.45** | **4.35** | **4.65** |

*Note: Scores represent a subjective evaluation based on the project's initial requirements, not official performance benchmarks.*

## 7. Demonstration

### Selected tool: Minikube

The following commands demonstrate how to create a local Kubernetes cluster and deploy a test application.

**Step 1. Start Minikube**

```bash
minikube start --driver=docker
```

**Step 2. Check cluster status**

```bash
minikube status
kubectl get nodes
```

**Step 3. Deploy a test application**

```bash
kubectl create deployment hello-minikube \
  --image=kicbase/echo-server:1.0
```

**Step 4. Verify the deployment**

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

**Step 5. Open Kubernetes Dashboard**

```bash
minikube dashboard
```

### Demo Recording

The demonstration should show:

1. Starting the Minikube cluster.
2. Checking Kubernetes nodes.
3. Deploying the test application.
4. Verifying the running Pod.
5. Opening Kubernetes Dashboard.

![Minikube Demo](../assets/minikube-demo.gif)

## 8. Final Recommendation

After evaluating Minikube, Kind, and K3d, Minikube is recommended as the primary local Kubernetes environment for the initial AsciiArtify Proof of Concept.

The main reasons are:

1. **Ease of use:** Minikube is easy to install and configure, making it suitable for developers without extensive DevOps experience.
2. **Built-in functionality:** Dashboard and addons simplify cluster management and troubleshooting.
3. **Scalability:** Multi-node support allows testing applications in different cluster configurations.
4. **Flexibility:** Multiple drivers and container runtimes provide flexibility for local development.
5. **Documentation:** Extensive documentation and community support reduce the learning curve.

Although K3d received the highest score in the evaluation matrix, Minikube is recommended because ease of adoption and built-in management features are more important during the initial development stage.

Kind can be introduced later for automated Kubernetes testing in CI/CD pipelines.

K3d remains a good alternative when minimizing local resource consumption becomes a priority.

## 9. References

- Minikube: https://minikube.sigs.k8s.io/docs/
- Kind: https://kind.sigs.k8s.io/
- K3d: https://k3d.io/
- Kubernetes: https://kubernetes.io/docs/
- Minikube GitHub: https://github.com/kubernetes/minikube
- Kind GitHub: https://github.com/kubernetes-sigs/kind
- K3d GitHub: https://github.com/k3d-io/k3d