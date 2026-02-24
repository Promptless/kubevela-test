# KubeVela Architecture Diagram

This Mermaid diagram shows how KubeVela fits into a modern CI/CD pipeline as the continuous delivery (CD) control plane.

```mermaid
flowchart LR
    subgraph CI["CI (Continuous Integration)"]
        direction TB
        CIP["CI Pipeline"]
        Jenkins["Jenkins"]
        GitLab["GitLab"]
        Other["..."]
    end

    subgraph KubeVela["KubeVela (CD Control Plane)"]
        direction LR
        Render["Render"]
        Orchestrate["Orchestrate"]
        Deploy["Deploy"]
        Render --> Orchestrate --> Deploy
    end

    subgraph Targets["Deployment Targets"]
        direction TB
        subgraph K8s["Kubernetes Clusters"]
            K8sCluster["☸ Kubernetes"]
        end
        subgraph Clouds["Clouds"]
            Azure["Microsoft Azure"]
            AWS["AWS"]
            Alibaba["Alibaba Cloud"]
        end
        subgraph Edge["IoT/Edge"]
            RaspberryPi["Raspberry Pi"]
            Arduino["Arduino"]
        end
    end

    CI --> KubeVela
    KubeVela --> K8s
    KubeVela --> Clouds
    KubeVela --> Edge
```

## How it works

1. **CI tools** (Jenkins, GitLab, etc.) build, test, and package your application.

2. **KubeVela** acts as the CD control plane with three stages:
   - **Render**: Transforms application definitions into deployable artifacts
   - **Orchestrate**: Coordinates workflow, policies, and multi-cluster strategies
   - **Deploy**: Pushes the application to target environments

3. **Deployment targets** include:
   - Kubernetes clusters
   - Cloud providers (Azure, AWS, Alibaba Cloud, etc.)
   - IoT/Edge devices (Raspberry Pi, Arduino, etc.)
