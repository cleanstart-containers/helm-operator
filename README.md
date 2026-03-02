# CleanStart Container for Helm-Operator

The Helm Operator is a Kubernetes operator that automates the deployment and management of Helm charts in a cluster. It enables declarative management of Helm releases through custom resources, providing automated installation, upgrades, and rollbacks of applications packaged as Helm charts. The CleanStart Helm-Operator image provides a production-ready, security-hardened container optimized for enterprise environments. Built on a minimal base OS with comprehensive security hardening, this image delivers reliable application execution with advanced security features.

**📌 Base Foundation:** Security-hardened, minimal base OS designed for enterprise containerized environments from CleanStart Registry.

**Image Path:** `ghcr.io/cleanstart-containers/helm-operator`

**Registry:** CleanStart Registry

---

## Overview

The Helm Operator is a Kubernetes operator that automates the deployment and management of Helm charts through declarative custom resources. It provides a GitOps-ready approach to managing Helm releases with automated lifecycle management. This CleanStart Helm-Operator container is part of the CleanStart application suite, featuring enterprise-grade security hardening, automated vulnerability management, and compliance with industry standards.

---

## About CleanStart

CleanStart is a comprehensive container registry providing security-hardened, enterprise-ready container images. Our images are designed with security-first principles, featuring minimal attack surfaces, regular security updates, and compliance with industry standards.

### About CleanStart Images

CleanStart images are built on secure, minimal base operating systems and optimized for production environments. Each image undergoes rigorous security testing, vulnerability scanning, and compliance validation to ensure enterprise-grade security and reliability.

---

## Key Features

Core capabilities and strengths of this container:

- **Security-First Design**: Built with minimal attack surfaces and security hardening
- **Enterprise Compliance**: Meets industry standards including FIPS, STIG, and CIS benchmarks
- **Regular Updates**: Automated security patches and vulnerability management
- **Multi-Architecture Support**: Available for AMD64 and ARM64 architectures
- **Production Ready**: Optimized for enterprise deployment and scaling
- **Comprehensive Documentation**: Detailed guides and best practices for each image
- Automated Helm chart deployment and management
- Declarative configuration through custom resources
- Automated upgrade and rollback capabilities
- GitOps-ready deployment workflows

---

## Common Use Cases

Typical scenarios where this container excels:

- Automated application deployment in Kubernetes clusters
- GitOps-based continuous delivery pipelines
- Multi-cluster application management
- Helm release lifecycle automation
- Declarative infrastructure management
- Continuous deployment workflows

---

## Quick Start

### Pull Latest Image

Download the container image from the registry:
```bash
docker pull ghcr.io/cleanstart-containers/helm-operator:latest
docker pull ghcr.io/cleanstart-containers/helm-operator:latest-dev
```

### Basic Run

Run the container with basic configuration:
```bash
docker run -it --name helm-operator-test ghcr.io/cleanstart-containers/helm-operator:latest-dev
```

### Production Deployment

Deploy with production security settings:
```bash
docker run -d --name helm-operator-prod \
  --read-only \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  ghcr.io/cleanstart-containers/helm-operator:latest
```

### Volume Mount

Mount local directory for persistent data:
```bash
docker run -v $(pwd)/data:/data ghcr.io/cleanstart-containers/helm-operator:latest
```

### Inspection

Inspect the environment:
```bash
docker inspect ghcr.io/cleanstart-containers/helm-operator:latest
```

---

## Configuration

### Environment Variables

Configuration options available through environment variables:

| Variable | Default | Description |
|----------|---------|-------------|
| `HELM_VERSION` | `v3.8.0` | Helm version to use |
| `WATCH_NAMESPACE` | - | Namespace to watch for custom resources |
| `OPERATOR_NAME` | `helm-operator` | Name of the operator |
| `LOG_LEVEL` | `info` | Logging level configuration |

---

## Security Best Practices

Recommended security configurations and practices:

- Use specific image tags for production deployments
- Configure RBAC policies appropriately
- Enable read-only root filesystem
- Run as non-root user
- Implement network policies
- Regular security updates and patches
- Use secure Helm repositories
- Monitor operator logs and activities

### Kubernetes Security Context

Recommended security context for Kubernetes deployments:
```yaml
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  runAsGroup: 1000
  readOnlyRootFilesystem: true
  allowPrivilegeEscalation: false
  capabilities:
    drop: ["ALL"]
```

---

## Architecture Support

CleanStart images support multiple architectures to ensure compatibility across different deployment environments:

- **AMD64**: Intel and AMD x86-64 processors
- **ARM64**: ARM-based processors including Apple Silicon and ARM servers

### Multi-Platform Images
```bash
docker pull --platform linux/amd64 ghcr.io/cleanstart-containers/helm-operator:latest
docker pull --platform linux/arm64 ghcr.io/cleanstart-containers/helm-operator:latest
```

---

## Resources

* **Official Documentation**: https://example.com/docs/helm-operator
* **Provenance / SBOM / Signature**: https://images.cleanstart.com/images/helm-operator
* **Docker Hub**: https://hub.docker.com/r/cleanstart/helm-operator
* **CleanStart All Images**: https://images.cleanstart.com
* **CleanStart Community Images**: https://hub.docker.com/u/cleanstart


---

## Vulnerability Disclaimer

CleanStart offers Docker images that include third-party open-source libraries and packages maintained by independent contributors. While CleanStart maintains these images and applies industry-standard security practices, it cannot guarantee the security or integrity of upstream components beyond its control.

Users acknowledge and agree that open-source software may contain undiscovered vulnerabilities or introduce new risks through updates. CleanStart shall not be liable for security issues originating from third-party libraries, including but not limited to zero-day exploits, supply chain attacks, or contributor-introduced risks.

**Security remains a shared responsibility:** CleanStart provides updated images and guidance where possible, while users are responsible for evaluating deployments and implementing appropriate controls.
