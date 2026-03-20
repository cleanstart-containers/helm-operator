# Helm-Operator Sample Project - Testing Guide

This is a simple project to test the `cleanstart/helm-operator:latest-dev` container image.

## Overview

Helm Operator is a helper binary packaged in this image. The container runs as a non-root user (`clnstrt`).

- **Image**: `cleanstart/helm-operator:latest-dev`
- **User**: `clnstrt` (non-root, UID 1000)
- **Entrypoint**: `helm-operator`

## Prerequisites

- Docker installed and running

## Testing the Image

### Step 1: Pull the Image

```bash
docker pull cleanstart/helm-operator:latest-dev
```

### Step 2: Display Help

```bash
docker run --rm cleanstart/helm-operator:latest-dev --help
```

This shows all available commands and options of `helm-operator`.

### Step 3: Check Version (if supported)

```bash
docker run --rm cleanstart/helm-operator:latest-dev --version
```

If the binary does not support `--version`, it will print an error; this is expected and does not indicate a problem with the image.

## Advanced Usage

### Interactive Shell Access

```bash
docker run -it --rm --entrypoint /bin/sh cleanstart/helm-operator:latest-dev
```

Inside the shell, you can run commands directly:
```sh
helm-operator --help
```

### Extended Tests

Run additional checks:

```bash
# 1) Show the current user and binary path
docker run --rm --entrypoint /bin/sh cleanstart/helm-operator:latest-dev -c 'whoami && which helm-operator'

# 2) Print environment variables relevant to TLS
docker run --rm --entrypoint /bin/sh cleanstart/helm-operator:latest-dev -c 'echo SSL_CERT_FILE=$SSL_CERT_FILE && ls -l /etc/ssl/certs | head -20'

# 3) Display help and capture exit code
docker run --rm cleanstart/helm-operator:latest-dev --help ; echo $?

# 4) Try version (may not be supported)
docker run --rm cleanstart/helm-operator:latest-dev --version || true

# 5) Show runtime OS details
docker run --rm --entrypoint /bin/sh cleanstart/helm-operator:latest-dev -c 'uname -a && cat /etc/os-release || true'
```

### Working Directory Mount (Optional)

Mount a local folder if you want to exchange files with the container:

```bash
mkdir -p helm-operator-test && cd helm-operator-test
docker run --rm -v "$(pwd)":/workspace:ro cleanstart/helm-operator:latest-dev --help
cd .. && rm -rf helm-operator-test
```

## Troubleshooting

### Permission Issues

The image runs as a non-root user (`clnstrt`). Ensure mounted volumes are readable by UID 1000 if you extend the image for local development.

### Network/Registry Issues

Ensure your environment can pull `cleanstart/helm-operator:latest-dev` from the registry.

### Common Errors

- Command not found: Ensure you did not override the entrypoint incorrectly and that you are invoking `helm-operator` (not `helm`).
- TLS or CA errors: Verify `SSL_CERT_FILE` is set (defaults inside the image) and your network can reach required endpoints.
- Permission denied on mounts: Fix host directory permissions to be readable by UID 1000.

## Cleanup

No resources are created; containers are run with `--rm` and removed on exit.
